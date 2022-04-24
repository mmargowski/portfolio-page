<script context="module">
  import {client} from "$lib/graphql-client"
  import {gql} from "graphql-request"

  import ProjectCard from "$lib/components/project-card.svelte";

  export const load = async () => {

    const query = gql`
      query GetProjects {
        projects {
          name
          slug
          description
          demo
          sourceCode
          image {
            url
          }
        }
      }
    `

    const { projects } = await client.request(query)

    return {
      props: {
        projects,
      },
    }

  }
</script>

<script>
  export let projects
</script>

<h1>Recent Projects by Me</h1>
{#each projects as {name, slug, description, image}}
  <ProjectCard {name} {description} url={image[0].url} {slug} />
{/each}

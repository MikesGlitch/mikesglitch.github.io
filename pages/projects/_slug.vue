<template>
  <article>
    <p>Post last updated: {{ project.updatedAt }}</p>
    <h1>{{ project.title }}</h1>
    <p>{{ project.description }}</p>

    <ul>
      <li v-for="link of project.toc" :key="link.id">
        <NuxtLink :to="`#${link.id}`">
          {{ link.text }}
        </NuxtLink>
      </li>
    </ul>
    <nuxt-content :document="project" />
  </article>
</template>

<script>
export default {
  async asyncData ({ $content, params }) {
    const project = await $content('projects', params.slug).fetch()

    return { project }
  }
}
</script>

<style>
  .nuxt-content h2 {
    font-weight: bold;
    font-size: 28px;
  }
  .nuxt-content h3 {
    font-weight: bold;
    font-size: 22px;
  }
  .nuxt-content p {
    margin-bottom: 20px;
  }
</style>

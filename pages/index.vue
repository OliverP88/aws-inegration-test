<template>
  <div class="p-4 mx-auto flex-col">
    <h1>Articles:</h1>
    <NuxtLink
      v-for="(link, i) of articles"
      :key="i"
      :to="`/blog/${link.slug}`"
      class="mr-2"
    >
      {{ link.slug | capitalize }}
    </NuxtLink>
  </div>
</template>

<script>
export default {
  filters: {
    capitalize (value) {
      if (!value) {
        return ''
      }
      value = value.toString()
      return value.charAt(0).toUpperCase() + value.slice(1)
    }
  },
  data () {
    return {
      articles: []
    }
  },
  async fetch () {
    this.articles = await this.$content('articles').fetch()
  }
}
</script>

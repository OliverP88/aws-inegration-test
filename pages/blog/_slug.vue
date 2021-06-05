<template>
  <div class="p-4">
    <article>
      <h1 class="title">
        {{ article.title }}
      </h1>
      <p class="date">
        Article last updated: {{ formatDate(article.updatedAt) }}
      </p>
      <img :src="article.img" :alt="article.alt">
      <p class="pb-4">
        {{ article.description }}
      </p>

      <nuxt-content :document="article" />

      <prev-next :prev="prev" :next="next" />
    </article>
  </div>
</template>

<script>
export default {
  async asyncData ({ $content, params }) {
    const article = await $content('articles', params.slug).fetch()

    const [prev, next] = await $content('articles')
      .only(['title', 'slug'])
      .sortBy('createdAt', 'asc')
      .surround(params.slug)
      .fetch()

    return {
      article,
      prev,
      next
    }
  },
  methods: {
    formatDate (date) {
      const options = { year: 'numeric', month: 'long', day: 'numeric' }
      return new Date(date).toLocaleDateString('en', options)
    }
  }
}
</script>

<style>
.title {
  font-size: 2.4rem;
  color: lightslategrey;
}
.date {
  font-size: 0.8rem;
}
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

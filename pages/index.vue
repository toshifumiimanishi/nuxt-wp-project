<template>
  <div class="container">
    <div>
      <logo />
      <h1 class="title">
        nuxt-wp-project
      </h1>
      <h2 class="subtitle">
        My outstanding Nuxt.js x WordPress project
      </h2>
      <div class="links">
        <a
          href="https://nuxtjs.org/"
          target="_blank"
          class="button--green"
        >
          Documentation
        </a>
        <a
          href="https://github.com/nuxt/nuxt.js"
          target="_blank"
          class="button--grey"
        >
          GitHub
        </a>
      </div>
      <article class="wp-article" v-for="post in posts" :key="post.id">
        <n-link :to="{ path: '/' + post.id }">
          <div class="wp-article_title">{{ post.title.rendered }}</div>
          <div class="wp-article_content" v-html="post.content.rendered"></div>
        </n-link>
      </article>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import Logo from '~/components/Logo.vue'

export default {
  data () {
    return {
      posts: []
    }
  },
  components: {
    Logo
  },
  created () {
    axios.get('http://localhost:8000/wp-json/wp/v2/posts/')
    .then(({ data }) => {
      this.posts = data
    })
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>

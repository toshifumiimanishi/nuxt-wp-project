<template>
  <div>
    <h2>{{ post.title.rendered }}</h2>
    <div v-html="post.content.rendered"></div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      post: {}
    }
  },
  async asyncData({ $axios, params, error, payload }) {
    if (payload) {
      return { post: payload }
    } else {
      const { data } = await $axios.get(`/posts/${params.id}`)
      return { post: data }
    }
  }
}
</script>

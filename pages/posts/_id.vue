<template>
  <div>
    <div class="wp-article_title">{{ post.title.rendered }}</div>
    <div class="wp-article_content" v-html="post.content.rendered"></div>
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
      return await $axios.get(`${$axios.defaults.baseURL}/posts/${params.id}`)
      .then(({ data }) => {
        return {
          post: data
        }
      })
    }
  }
}
</script>

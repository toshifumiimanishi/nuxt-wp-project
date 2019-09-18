<template>
  <div>
    <div class="wp-article_title">{{ post.title.rendered }}</div>
    <div class="wp-article_content" v-html="post.content.rendered"></div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data () {
    return {
      post: {}
    }
  },
  async asyncData({ params, error, payload }) {
    if (payload) {
      return { post: payload }
    } else {
      return await axios.get(`http://nuxt-wp-project.oops.jp/wp-json/wp/v2/posts/${params.id}`)
      .then(({ data }) => {
        return {
          post: data
        }
      })
    }
  }
}
</script>

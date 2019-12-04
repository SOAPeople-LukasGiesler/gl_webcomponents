<template>
    <div class="posts">
        <h1>Posts</h1>
        This file will display all the posts.

        <div v-for="post in posts" v-bind:key="post.title">
            <p>
                <span><b>{{ post.title }}</b></span><br />
                <span>{{ post.description }}</span>
                <ui5-button>{{ post.title }}</ui5-button>
            </p>
        </div>
    </div>
</template>

<script>
import PostsService from '@/services/PostsService'
import '@ui5/webcomponents/dist/Button'

export default {
  name: 'posts',
  data () {
    return {
      posts: []
    }
  },
  mounted () {
    this.getPosts()
  },
  methods: {
    async getPosts () {
      const response = await PostsService.fetchPosts()
      this.posts = response.data
    }
  }
}
</script>

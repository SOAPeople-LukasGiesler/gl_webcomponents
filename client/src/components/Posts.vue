<template>
    <div class="posts">
        <ui5-shellbar
          primary-title="Endor"
          profile=""
          show-notifications
          show-product-switch
          show-co-pilot
          @menuItemClick="getMenuItem"
        >
          <ui5-li slot="menuItems" id="mi_home">Home</ui5-li>
        </ui5-shellbar>
        <!-- <div v-for="post in posts" v-bind:key="post.title"> -->
            <ui5-list id="myList" class="full-width">
              <ui5-li v-for="post in posts" v-bind:key="post.title" :description="post.description" info="In-stock">{{ post.title }}</ui5-li>
            </ui5-list>
        <!-- </div> -->
    </div>
</template>

<script>
import PostsService from '@/services/PostsService'
import '@ui5/webcomponents/dist/Button'
import '@ui5/webcomponents-fiori/dist/ShellBar'
import '@ui5/webcomponents/dist/List'
import '@ui5/webcomponents/dist/StandardListItem'

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
    },

    getMenuItem (event) {
      if (event.detail.item.id === 'mi_home') {
        this.$router.push('/')
      }
    }
  }
}
</script>

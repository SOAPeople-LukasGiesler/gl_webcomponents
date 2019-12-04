<template>
  <div class="main_container">
    <ui5-shellbar
      primary-title="Endor"
      profile=""
      show-notifications
      show-product-switch
      show-co-pilot
      @menuItemClick="getMenuItem"
    >
      <ui5-li slot="menuItems" id="mi_posts">Posts</ui5-li>
    </ui5-shellbar>
    <ui5-tabcontainer class="full-width" collapsed fixed show-overflow>
      <ui5-tab text="Home"></ui5-tab>
      <ui5-tab text="Page1"></ui5-tab>
    </ui5-tabcontainer>
  </div>
</template>

<script>
import '@ui5/webcomponents-fiori/dist/ShellBar'
import '@ui5/webcomponents/dist/ListItem'
import '@ui5/webcomponents/dist/TabContainer'
import '@ui5/webcomponents/dist/Tab'

export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  methods: {
    getMenuItem (event) {
      console.log(event.detail.item.id)
      if (event.detail.item.id === 'mi_posts') {
        this.$router.push('posts')
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.main_container{
  margin: 0px;
  padding: 0px;
  height: 100%;
}
</style>

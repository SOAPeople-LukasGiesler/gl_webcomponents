<template>
  <div>
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
    <ui5-tabcontainer class="full-width" fixed show-overflow>
      <ui5-tab text="Home">
        <ui5-textarea placeholder="post xml here" @change="ta_changed"></ui5-textarea>
      </ui5-tab>
      <ui5-tab text="Page1"></ui5-tab>
    </ui5-tabcontainer>
  </div>
</template>

<script>
import '@ui5/webcomponents-fiori/dist/ShellBar'
import '@ui5/webcomponents/dist/ListItem'
import '@ui5/webcomponents/dist/TabContainer'
import '@ui5/webcomponents/dist/Tab'
import '@ui5/webcomponents/dist/Card'
import '@ui5/webcomponents/dist/Label'
import '@ui5/webcomponents/dist/TextArea'

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
    },
    ta_changed (event) {
      var parser = require('fast-xml-parser')
      var he = require('he')
      var options = {
        attributeNamePrefix: '@_',
        attrNodeName: 'attr',
        textNodeName: '#text',
        ignoreAttributes: true,
        ignoreNameSpace: false,
        allowBooleanAttributes: false,
        parseNodeValue: true,
        parseAttributeValue: false,
        trimValues: true,
        cdataTagName: '__cdata',
        cdataPositionChar: '\\c',
        localRange: '',
        parseTrueNumberOnly: false,
        arrayMode: false,
        attrValueProcessor: (val, attrName) => he.decode(val, {isAttributeValue: true}),
        tagValueProcessor: (val, tagName) => he.decode(val),
        stopNodes: ['parse-me-as-string']
      }
      var tObj = parser.getTraversalObj(event.srcElement.value, options)
      var jsonObj = parser.convertToJson(tObj, options)
      console.log(jsonObj)
      console.log(jsonObj.note)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.card-content{
  display: flex;
  justify-content: flex-start;
  flex-wrap: wrap;
}

.medium{
  width: 25%;
  margin: 2px;
  height: 50%;
}

.full-width{
  width: 100%;
  height: 100%;
}

.card-content-child{
  align-items: flex-start;
}
</style>

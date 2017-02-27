<template>
  <div id="app">
    <h1 v-text='title'></h1>
    <!-- 父组件传给子组件的方式1 ： v-on:事件="addNew"-->
    <input type="" v-model="newItem" v-on:keyup.enter="addNew">
    <ul>
      <li v-for="item in items" :class="{finished :item.isFinished}" v-on:click="toggleFinish(item)">
        {{item.label}}
      </li>
    </ul>
    <component-a msgfromfather='father' v-on:child="listenFromChild"></component-a>
    <p>{{ childWords }}</p>
    <router-view></router-view>
  </div>
</template>

<script>
import Store from './store'
import ComponentA from './components/test1'
export default {
  data: function () {
    return {
      title: 'this is title',
      items: Store.fetch(),
      newItem: '',
      childWords: ''
    }
  },
  methods: {
    toggleFinish: function (item) {
      item.isFinished = !item.isFinished
    },
    addNew: function () {
      this.items.push({
        label: this.newItem,
        isFinished: false
      })

      this.newItem = ''
      this.$broadcast('addNew', this.items)
    }
    // 子组件传给父组件的方式1
    // listenFromChild: function (msg) {
    //   this.childWords = msg
    // }
  },
  // 子组件传给父组件的方式2
  events: {
    listenFromChild: function (msg) {
      this.childWords = msg
    }
  },
  watch: {
    items: {
      handler: function (items) {
        Store.save(items)
      },
      deep: true
    }
  },
  components: { ComponentA },
  name: 'app'
}
</script>

<style>
.finished{
  color: red;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

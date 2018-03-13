<template>
  <!-- <router-view/> -->
  <div id="app">
    <h1 v-text="title"></h1>
    <input id="add-input" v-model="newItem" @keyup.enter="addNew">
    <ul>
      <li v-for="(item,index) in items" v-bind:key="index">
       <todo-item v-bind="{item: item,index: index}" v-on:delete="deleteHandler"></todo-item>
      </li>
    </ul>
  </div>
</template>

<script>
import Store from './store'
import todoItem from './components/TodoItem'
export default {
  name: 'App',
  data () {
    return {
      title: 'This is a todoList',
      items: Store.fetch(),
      newItem: ''
    }
  },
  components: { todoItem },
  watch: {
    items: {
      handler: function (items) {
        Store.save(items)
      },
      deep: true
    }
  },
  methods: {
    addNew: function () {
      this.items.push({
        label: this.newItem,
        isFinished: false,
        showDelete: false
      })
      this.newItem = ''
    },
    deleteHandler: function (item) {
      var index = this.items.indexOf(item)
      this.items.splice(index, 1)
    }
  }
}
</script>

<style>
#app {
  margin: 0 auto;
  width: 400px;
  -moz-user-select: none;
  -webkit-user-select: none;
  -ms-user-select: none;
  -o-user-select: none;
  user-select: none;
}
#add-input {
  width: 350px;
  height: 30px;
}
li {
  list-style: none;
}
</style>

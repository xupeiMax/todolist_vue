<template>
  <h3 @mouseenter="itemEnter(item)" @mouseleave="itemLeave(item)">
    <input type="checkbox" @click="toggleFinish(item)" v-model="item.isFinished">
    <p class="item-label" @click="toggleFinish(item)" :class="{finished:item.isFinished}">{{ index + 1 }}.{{item.label}}</p>
    <p class="item-status" v-if="item.isFinished">finished</p>
    <p class="item-delete" v-if="item.showDelete" @click="deleteItem(item)">Delete</p>
  </h3>
</template>

<script>
export default {
  name: 'todoItem',
  data () {
    return { }
  },
  props: ['item', 'index'],
  methods: {
    toggleFinish: function (item) {
      item.isFinished = !item.isFinished
      item.showDelete = true
    },
    itemEnter: function (item) {
      item.showDelete = true
    },
    itemLeave: function (item) {
      item.showDelete = false
    },
    deleteItem: function (item) {
      this.$emit('delete', item)
    }
  }
}
</script>

<style scoped>
p {
  display: inline;
}
.finished {
  text-decoration: line-through;
}
.item-status {
  background-color: red;
  color: #fff;
  font-size: 12px;
  padding: 0 5px;
}
.item-delete {
  text-decoration: underline;
  color: gray;
  font-size: 12px;
  cursor: pointer;
}
</style>

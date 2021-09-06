<template>
  <li>
    <label>
      <input type="checkbox" :checked="qwe.done" @click="handleCheck(qwe.id)" />
      <span>{{ qwe.title }}</span>
    </label>
    <button class="btn btn-danger" @click="handelDelete(qwe.id)">删除</button>
  </li>
</template>

<script>
import pubsub from 'pubsub-js'
export default {
  name: 'VItem666',
  // declear receive todo obj
  props: ['qwe', 'deleteTodo'],
  methods: {
    handleCheck(id) {
      this.$bus.$emit('changeChecked', id)
    },
    handelDelete(id) {
      if (confirm('Are you sure you want to delete')) pubsub.publish('deleteTodo', id)
    },
  },
}
</script>

<style scoped>
/*item*/
li {
  list-style: none;
  height: 36px;
  line-height: 36px;
  padding: 0 5px;
  border-bottom: 1px solid #ddd;
}

li label {
  float: left;
  cursor: pointer;
}

li label li input {
  vertical-align: middle;
  margin-right: 6px;
  position: relative;
  top: -1px;
}

li button {
  float: right;
  display: none;
  margin-top: 3px;
}

li:before {
  content: initial;
}

li:last-child {
  border-bottom: none;
}
li:hover {
  background-color: #ddd;
}
li:hover button {
  display: block;
}
</style>

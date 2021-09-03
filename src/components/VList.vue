<template>
  <ul class="todo-main">
   <VItem v-for="(todoObj) in todos" :key="todoObj.id" :qwe="todoObj"></VItem>
  </ul>
</template>

<script>
import VItem from './VItem'
export default {
  name: 'VList',
  components: { VItem },
  data() {
    return {
      todos: [
        { id: '001', title: '抽烟', done: true },
        { id: '002', title: '喝酒', done: false },
        { id: '003', title: '开车', done: true },
      ],
    }
  },
}
</script>

<style scoped>
.todo-main {
  margin-left: 0px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding: 0px;
}

.todo-empty {
  height: 40px;
  line-height: 40px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding-left: 5px;
  margin-top: 10px;
}
</style>

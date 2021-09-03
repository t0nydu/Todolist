<template>
  <ul class="todo-main">
    <VItem></VItem>
  </ul>
</template>

<script>
import VItem from './VItem'
export default {
  name: 'VList',
  components: { VItem },
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

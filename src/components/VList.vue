<template>
  <ul class="todo-main">
    <transition-group appear name="animate__animated animate__bounce" enter-active-class="animate__bounceInLeft" leave-active-class="animate__backOutUp">
      <VItem v-for="todoObj in todos" :key="todoObj.id" :qwe="todoObj"></VItem>
    </transition-group>
  </ul>
</template>

<script>
import 'animate.css'
import VItem from './VItem'
export default {
  name: 'VList',
  components: { VItem },
  props: ['todos'],
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

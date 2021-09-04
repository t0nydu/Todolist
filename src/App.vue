<template>
  <!-- 拆，先拆结构，再拆样式 -->
  <div id="root">
    <div class="todo-container">
      <div class="todo-wrap">
        <VHeader :addTodo="addTodo"></VHeader>
        <VList :todos="todos" :changeChecked="changeChecked" :deleteTodo="deleteTodo"></VList>
        <VFooter :todos="todos" :checkAll="checkAll" :clearAll="clearAll"></VFooter>
      </div>
    </div>
  </div>
</template>

<script>
import VHeader from './components/VHeader'
import VFooter from './components/VFooter'
import VList from './components/VList'

export default {
  name: 'App',
  components: {
    VHeader,
    VFooter,
    VList,
  },
  data() {
    return {
      todos: [
        { id: '001', title: '抽烟', done: true },
        { id: '002', title: '喝酒', done: false },
        { id: '003', title: '开车', done: true },
      ],
    }
  },
  methods: {
    addTodo(x) {
      this.todos.unshift(x) // -->重新解析模板
    },
    changeChecked(id) {
      this.todos.forEach((item) => {
        if (item.id === id) {
          item.done = !item.done
        }
      })
    },
    deleteTodo(id) {
      this.todos.forEach((item, index) => {
        if (item.id === id) {
          this.todos.splice(index, 1)
        }
      })
    },
    checkAll(status) {
      this.todos.forEach((item) => {
        item.done = status
      })
    },
    clearAll() {
      this.todos = this.todos.filter((item) => !item.done)
      //  this.todos.forEach((item, index) => {
      //     if (item.done) {
      //       this.todos.splice(index, 1)
      //     }
      //   })
    },
  },
}
</script>

<style>
/*base*/
body {
  background: #fff;
}

.btn {
  display: inline-block;
  padding: 4px 12px;
  margin-bottom: 0;
  font-size: 14px;
  line-height: 20px;
  text-align: center;
  vertical-align: middle;
  cursor: pointer;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
  border-radius: 4px;
}

.btn-danger {
  color: #fff;
  background-color: #da4f49;
  border: 1px solid #bd362f;
}

.btn-danger:hover {
  color: #fff;
  background-color: #bd362f;
}

.btn:focus {
  outline: none;
}

.todo-container {
  width: 600px;
  margin: 0 auto;
}
.todo-container .todo-wrap {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}
</style>

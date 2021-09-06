<template>
  <!-- 拆，先拆结构，再拆样式 -->
  <div id="root">
    <div class="todo-container">
      <div class="todo-wrap">
        <VHeader :addTodo="addTodo"></VHeader>
        <VList :todos="todos"></VList>
        <VFooter :todos="todos" @checkAll="checkAll" @clearAll="clearAll"></VFooter>
      </div>
    </div>
  </div>
</template>

<script>
import pubsub from 'pubsub-js'
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
      todos: JSON.parse(localStorage.getItem('todos')) || [],
    }
  },
  methods: {
    addTodo(x) {
      this.todos.unshift(x) // -->重新解析模板
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
  watch: {
    todos: {
      deep: true,
      handler(value) {
        localStorage.setItem('todos', JSON.stringify(value))
      },
    },
  },
  mounted() {
    this.$bus.$on('changeChecked', (id) => {
      this.todos.forEach((item) => {
        if (item.id === id) {
          item.done = !item.done
        }
      })
    })
    this.pubId = pubsub.subscribe('deleteTodo', (_, id) => {
      this.todos.forEach((item, index) => {
        if (item.id === id) {
          this.todos.splice(index, 1)
        }
      })
    })
    // this.$bus.$on('deleteTodo', (id) => {
    //   this.todos.forEach((item, index) => {
    //     if (item.id === id) {
    //       this.todos.splice(index, 1)
    //     }
    //   })
    // })
  },
  beforeDestroy() {
    this.$bus.$off('changeChecked')
    pubsub.unsubscribe(this.pubId)
    // this.$bus.$off('deleteTodo')
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
.btn-edit{
  color: #fff;
  background-color: skyblue;
  border: 1px solid rgb(9, 178, 245);
  margin-right: 6px;
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

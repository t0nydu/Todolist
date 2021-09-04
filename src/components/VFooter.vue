<template>
  <div class="todo-footer" v-show="total">
    <label>
      <input type="checkbox" v-model="isAll" />
      <!-- <input type="checkbox" v-bind:checked="isAll" v-on:click="_checkAll"/> -->
    </label>
    <span>
      <span>已完成{{ doneTotal }}</span> / 全部{{ total }}
    </span>
    <button class="btn btn-danger" @click="_clearAll">清除已完成任务</button>
  </div>
</template>

<script>
export default {
  name: 'VFooter',
  props: ['todos'],
  methods: {
    _clearAll() {
      if (confirm('确定要清空所有完成的吗')) {
        // this.clearAll()
        this.$emit("clearAll")
      }
    },
  },
  computed: {
    total() {
      return this.todos.length
    },
    doneTotal() {
      return this.todos.filter((i) => i.done).length
      // return this.todos.reduce((v,i)=>v+=i.done?1:0,0)
    },
    isAll: {
      get() {
        return this.doneTotal === this.total && this.total > 0
      },
      set(value) {
        // this.checkAll(value)
        this.$emit('checkAll', value)
      },
    },
  },
}
</script>

<style>
/*footer*/
.todo-footer {
  height: 40px;
  line-height: 40px;
  padding-left: 6px;
  margin-top: 5px;
}

.todo-footer label {
  display: inline-block;
  margin-right: 20px;
  cursor: pointer;
}

.todo-footer label input {
  position: relative;
  top: -1px;
  vertical-align: middle;
  margin-right: 5px;
}

.todo-footer button {
  float: right;
  margin-top: 5px;
}
</style>

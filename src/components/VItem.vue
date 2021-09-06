<template>
  <li>
    <label>
      <input type="checkbox" :checked="qwe.done" @click="handleCheck(qwe.id)" />
      <span v-show="!this.isEdit">{{ qwe.title }}</span>
    </label>
    <input ref="inputTitle" type="text" v-show="this.isEdit" @blur="doneEdit($event)" @keyup.enter="doneEdit" :value="qwe.title" />
    <button class="btn btn-danger" @click="handelDelete(qwe.id)">删除</button>
    <button class="btn btn-edit" v-show="!this.isEdit" @click="handelEdit">编辑</button>
  </li>
</template>

<script>
import pubsub from 'pubsub-js'
export default {
  name: 'VItem666',
  data() {
    return {
      isEdit: false,
    }
  },
  // declear receive todo obj
  props: ['qwe', 'deleteTodo'],
  methods: {
    handleCheck(id) {
      this.$bus.$emit('changeChecked', id)
    },
    handelDelete(id) {
      if (confirm('Are you sure you want to delete')) pubsub.publish('deleteTodo', id)
    },
    handelEdit() {
      this.isEdit = !this.isEdit
      // setTimeout(() => {
      //   this.$el.querySelector('li>input').focus()
      // }, 20)
      // dom更新完毕，调用函数
      this.$nextTick(()=>{
        this.$refs.inputTitle.focus()
      })
    },
    doneEdit(e) {
      this.isEdit = false
      const userInput = e.target.value //this.$el.querySelector('li>input').value
      if (userInput.trim() === '') return alert('输入不能为空')
      this.qwe.title = userInput
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

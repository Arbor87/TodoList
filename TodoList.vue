<template>
  <div class="todo-list">
    <h1>TodoList</h1>
    <div class="input-container">
      <!-- 输入框绑定newTodo，回车也能添加 -->
      <input 
        type="text" 
        placeholder="Add a new todo" 
        v-model="newTodo"
        @keyup.enter="addTodo"
      >
      <button class="add-button" @click="addTodo">Add</button>
    </div>
    <div class="todos-container">
      <ul>
        <!-- 修正循环变量名：todos → todo（单数更语义化） -->
        <li v-for="(todo, index) in todos" :key="index">
          {{ todo }}
        </li>
      </ul>
      <!-- 空状态提示 -->
      <p v-if="todos.length === 0">暂无待办事项，添加一个吧～</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TodoList',
  // 只接收父组件传递的todos，子组件不自己定义todos数据
  props: {
    todos: {
      type: Array,
      required: true,
      default: () => [] // 兜底默认值
    }
  },
  data() {
    return {
      newTodo: '' // 仅存储输入框的临时内容
    }
  },
  methods: {
    addTodo() {
      // 校验：去除首尾空格，空内容不添加
      const todoText = this.newTodo.trim()
      if (!todoText) {
        alert('请输入待办事项内容！')
        return
      }
      // 向父组件派发事件，传递要添加的内容
      this.$emit('add-todo', todoText)
      // 清空输入框
      this.newTodo = ''
    }
  }
}
</script>

<style scoped>
.todo-list {
  max-width: 500px;
  margin: 0 auto;
  padding: 20px;
}
.input-container {
  margin: 20px 0;
  display: flex;
  gap: 10px;
}
input {
  flex: 1;
  padding: 8px 12px;
  border: 1px solid #ddd;
  border-radius: 4px;
}
.add-button {
  padding: 8px 20px;
  background: #42b983;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
.add-button:hover {
  background: #359469;
}
.todos-container {
  text-align: left;
}
ul {
  list-style: none;
  padding: 0;
  margin: 0 0 10px 0;
}
li {
  padding: 10px;
  border-bottom: 1px solid #eee;
}
</style>
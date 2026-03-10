<template>
  <!-- 引入TodoList子组件，传递数据+监听事件 -->
  <TodoList 
    :todos="todoList" 
    @add-todo="handleAddTodo"
  />
</template>

<script>
// 引入TodoList组件（注意路径是否正确）
import TodoList from './components/TodoList.vue'

export default {
  name: 'App',
  components: {
    // 注册子组件
    TodoList
  },
  data() {
    return {
      // 父组件统一管理todos数据（核心数据放在父组件，保证单向数据流）
      todoList: []
    }
  },
  methods: {
    // 处理子组件派发的添加事件
    handleAddTodo(newTodo) {
      // 把新的待办事项添加到数组中
      this.todoList.push(newTodo)
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
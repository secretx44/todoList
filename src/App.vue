

<template>
  <div class="d-flex text-center">
    <h1 class="m-auto">Simple Todo List Using Vuejs</h1>
  </div>
  <br>
  <div class="text-center">
    <h1 class="text-center my-3">Todo List</h1>
    <form @submit.prevent="addTodo">
      <input class="addNew" type="text" v-model="newTodo" placeholder="Add new todo">
      <button class="btn btn-secondary" type="submit">Add</button>
    </form>
    <ul v-if="todos.length > 0">
      <li v-for="(todo, index) in todos" :key="index" class="lists">
        <input class="check" type="checkbox" v-model="todo.completed">
        <span :class="{ 'completed': todo.completed }">{{ todo.text }}</span>
        <button @click="removeTodo(index)" class="btn btn-danger">
          <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-trash" viewBox="0 0 16 16">
            <path d="M5.5 5.5A.5.5 0 0 1 6 6v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5zm2.5 0a.5.5 0 0 1 .5.5v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5zm3 .5a.5.5 0 0 0-1 0v6a.5.5 0 0 0 1 0V6z"/>
            <path fill-rule="evenodd" d="M14.5 3a1 1 0 0 1-1 1H13v9a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V4h-.5a1 1 0 0 1-1-1V2a1 1 0 0 1 1-1H6a1 1 0 0 1 1-1h2a1 1 0 0 1 1 1h3.5a1 1 0 0 1 1 1v1zM4.118 4 4 4.059V13a1 1 0 0 0 1 1h6a1 1 0 0 0 1-1V4.059L11.882 4H4.118zM2.5 3V2h11v1h-11z"/>
          </svg>
        </button>
      </li>
    </ul>
    <p v-else>No todos yet!</p>
    <p>Total: {{ totalTodos }}</p>
    <p>Completed: {{ completedTodos }}</p>
  </div>
</template>

<script>
import 'bootstrap-vue/dist/bootstrap-vue.css'
import 'bootstrap/dist/css/bootstrap.css'

export default {
  data() {
    return {
      todos: [
        { text: 'Sample Todo App', completed: false },
        { text: 'Using VUE.JS', completed: false },
        { text: 'Made by Jn Gdt', completed: false }
      ],
      newTodo: ''
    }
  },
methods: {
  addTodo() {
    if (this.newTodo.trim() !== '') {
      const exists = this.todos.some(todo => todo.text === this.newTodo)
      if (exists) {
        alert('Item already exists in the list!')
      } else {
        this.todos.push({ text: this.newTodo, completed: false })
        this.newTodo = ''
      }
    }
  },
  removeTodo(index) {
    this.todos.splice(index, 1)
  }
},
  computed: {
    totalTodos() {
      return this.todos.length
    },
    completedTodos() {
      return this.todos.filter(todo => todo.completed).length
    }
  }
}
</script>

<style scoped>
.completed {
  text-decoration: line-through;
}
.addNew {
  width: 300px;
  height: 30px;
  border-radius: 5px;
  border: none;
  outline: none;
  padding: 5px;
}
</style>
<template>
  <div id="app">
    <TodoList v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
    import TodoList from './components/TodoList'; 
export default {
  name: 'App',
  components: {
    TodoList
  },
  data() {
    return {
      todos:[]
    }
  },
  methods: {
    fetchTodos() {
      fetch('http://localhost:8001/todos')
      .then(response => response.json())
      // .then(console.log)
      .then(todos => this.todos = todos)
    },
    deleteTodo(id){
      this.todos = this.todos.filter(todo => todo.id != id)
      fetch(`http://localhost:8001/todos/${id}`, {
        method: 'DELETE'
      })
    }
  },
    mounted(){
      this.fetchTodos()
    }
}
</script>

<style>

</style>

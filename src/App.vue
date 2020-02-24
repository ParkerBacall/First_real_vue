<template>
  <div id="app">
    <AddTodo v-on:add-todo="createTodo"/>
    <TodoList v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
    import TodoList from './components/TodoList'; 
    import AddTodo from './components/AddTodo'; 
export default {
  name: 'App',
  components: {
    TodoList,
    AddTodo
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
    },
    createTodo(newTodo){
      console.log(newTodo)
      this.todos = [...this.todos, newTodo]
      fetch('http://localhost:8001/todos/', {
         method: 'POST',
         headers:{
           'content-type': 'application/json'
         },
         body: JSON.stringify(newTodo)
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

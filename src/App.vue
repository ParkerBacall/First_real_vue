<template>
  <div id="app">
    <SearchBar/>
    <AddTodo v-on:add-todo="createTodo"/>
    <TodoList v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
    import TodoList from './components/TodoList'; 
    import AddTodo from './components/AddTodo'; 
    import SearchBar from './components/SearchBar'; 
export default {
  name: 'App',
  components: {
    TodoList,
    AddTodo,
    SearchBar
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
      .then(res => console.log(res))
      .catch(err => console.log(err))
    },
    createTodo(newTodo){
      this.todos = [...this.todos, newTodo]
      fetch('http://localhost:8001/todos/', {
         method: 'POST',
         headers:{
           'content-type': 'application/json'
         },
         body: JSON.stringify(newTodo)
      })
       .then(res => console.log(res))
      .catch(err => console.log(err))
    }
  },

    mounted(){
      this.fetchTodos()
    }
}
</script>

<style>

</style>

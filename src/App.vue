<template>
  <div id="app">
    <SearchBar v-bind:searchTerm="searchTerm" v-on:update-search-term="updateSearchTerm"/>
    <AddTodo v-on:add-todo="createTodo"/>
    <TodoList v-on:patch-todo="patchTodo" v-bind:todos="updateSearchTerm(searchTerm)" v-on:del-todo="deleteTodo"/>
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
      todos:[],
      searchTerm: ""
    }
  },
  methods: {

    fetchTodos() {
      fetch('http://localhost:8001/todos')
      .then(response => response.json())
      .then(todos => todos.sort(function(a, b) { 
       return a.id - b.id  ||  a.name.localeCompare(b.name)
      }))
      .then(todos => this.todos = todos)
    },

    deleteTodo(id){
      this.todos = this.todos.filter(todo => todo.id != id)
      fetch(`http://localhost:8001/todos/${id}`, {
        method: 'DELETE'
      })
      .then(res => res.json())
      .then(console.log)
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
      .then(res => res.json())
      .then(console.log)
      .catch(err => console.log(err))
    },
    
    patchTodo(id, title, text){
       fetch(`http://localhost:8001/todos/${id}`, {
         method: 'PUT',
           headers:{
              'content-type': 'application/json'
           },
            body: JSON.stringify({title, text})
         })
          .then(res => res.json())
          .then(todo => {
            [...this.todos.filter(todo => todo.id !== id), todo]
          })
          .catch(err => console.log(err))
       },
   
    updateSearchTerm(newSearchTerm){
        this.searchTerm = newSearchTerm
        return this.todos.filter(todo => {
          return todo.title.includes(newSearchTerm) || todo.text.includes(newSearchTerm)
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

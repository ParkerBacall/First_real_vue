<template>
  <div id="todoList">
    <div v-bind:key="todo.id" v-for="todo in todos">
      <Todo v-bind:todo="todo" 
      v-on:del-todo="$emit('del-todo', todo.id)"
      v-on:patch-todo="$emit('patch-todo', todo.id, todo.title, todo.text)"
      />
    </div>
  </div>
</template>

<script>
import Todo from './Todo'
export default {
    name: "TodoList",
     components:{
         Todo
    },
    props: ["todos"]
   
}
</script>

<style lang="css" scoped>
    #todoList{
        display: flex;
        justify-content: space-between;
        flex-wrap: wrap;
        padding: 35px;
    }
</style>
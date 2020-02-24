<template>
    <div id='todo' v-if=!this.showUpdateForm>       
        <h3>{{todo.title}}</h3>
        <p>{{todo.text}}</p>
        <button v-on:click="$emit('del-todo', todo.id)" >delete</button>
        <button v-on:click="showUpdate" >update</button>
    </div>
    <div v-else>
        <UpdateTodo v-on:patch-todo="$emit('patch-todo', todo.id, todo.title, todo.text)" v-bind:todo="todo" v-on:toggle="showUpdate"/>
    </div>
</template>


<script>
import UpdateTodo from "./UpdateTodo";
export default {
    name: "Todo",
    props: ["todo"],
    components:{
        UpdateTodo,
    },
    data() {
    return {
      showUpdateForm: false
    }
},
methods: {
    showUpdate(){
        this.showUpdateForm = !this.showUpdateForm
    }
}
}

</script>

<style lang="css" scoped>
    #todo{
        padding: 4px;
        box-shadow: 0px 0px 4px #666;
    }
</style>
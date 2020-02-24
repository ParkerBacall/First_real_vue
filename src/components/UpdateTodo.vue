<template>
    <div  id='update-todo-form'>
        <form @submit="updateTodo(todo.id, todo.title, todo.text)">
            <input type="text" v-model="todo.title" name="title" placeholder="todo title">
            <input type="text" v-model="todo.text" name="text" placeholder="todo text">
            <button v-on:click="$emit('toggle')" >back</button>
            <input type="submit">
        </form>
    </div>
</template>

<script>
export default {
    name: 'UpdateTodo',
    props: ['todo'],

    methods:{
        updateTodo(id, title, text){
            event.preventDefault();
            this.$emit('patch-todo', id, text, title)
            this.$emit('toggle')
        }
    }
}
</script>

<style lang="css">

    #update-todo-form{
        padding: 4px;
        box-shadow: 0px 0px 4px #666;
        width: 100px;
        display: flex;
        justify-content: center;
        flex-wrap: wrap;
    }
    input{
        width: 60px;
        height: 30px;
    }
    btn{
        padding: 4px
    }
</style>

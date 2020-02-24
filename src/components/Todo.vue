<template>
    <div id='todo'> 
        <h3>{{todo.title}}</h3>
        <p>{{todo.text}}</p>
        <button v-on:click="$emit('del-todo', todo.id)" >delete</button>
        <button v-on:click="$emit('update-todo', todo.id)" >update</button>
    </div>
</template>

<script>
export default {
    name: "Todo",
    props: ["todo"]
}
</script>

<style lang="css" scoped>
    #todo{
        padding: 4px;
        box-shadow: 0px 0px 4px #666;
    }
</style>
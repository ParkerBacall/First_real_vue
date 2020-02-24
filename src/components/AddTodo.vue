<template>
    <div  id='add-todo-form'>
        <form @submit="addTodo">
            <input type="text" v-model="title" name="title" placeholder="todo title">
            <input type="text" v-model="text" name="text" placeholder="todo text">
            <input type="submit">
        </form>
    </div>
</template>

<script>
export default {
    name: 'AddTodo',
    props: ["title","text"],
        methods: {
            addTodo(e){
                e.preventDefault()
                const newTodo ={ 
                    title: this.title,
                    text: this.text
                }
            this.$emit('add-todo', newTodo)
            this.title=""
            this.text=""
            }
        }
}
</script>

<style lang="css" scoped>
    #add-todo-form{
        display: flex;
        justify-content: center;
    }
</style>
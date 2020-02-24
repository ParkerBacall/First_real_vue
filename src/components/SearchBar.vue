<template>
    <div id='search-div'>
        <input type="text" placeholder="search for a todo by title or text">
    </div>
</template>

<script>
export default {
    name: "SearchBar"
}
</script>

<style lang="css" scoped>

    #search-div{
        display: flex;
        justify-content: center;
        padding: 15px;
    }

    input{
        width: 200px;
        height: 25px;
        padding: 5px;
        box-shadow: 0px 0px 4px #666;
    }
</style>
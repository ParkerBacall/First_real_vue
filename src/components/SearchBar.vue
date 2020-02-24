<template>
    <div id='search-div'>
        <form>
        <input 
            @input="emitSearchTerm"
            type="text" 
            name="searchTerm"
            :value=searchTerm
            placeholder="search for a todo by title or text"/>
         </form>
    </div>
</template>

<script>
export default {
    name: "SearchBar",
    props: ["searchTerm"],


methods: {
    emitSearchTerm(e){
        this.$emit('update-search-term', e.target.value)
    }
    }

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
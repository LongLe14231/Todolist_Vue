<template>
    <div>
        <div v-bind:key="x.id" v-for="x in todos">
            
            <TodosItem v-bind:todo="x" v-on:del-todo="$emit('del-todo',x.id)"/>
        </div>
    </div>
</template>


<script>
    import TodosItem from './TodosItem.vue';
    export default {
        name: "Todos",
        components:{
            TodosItem
        },
        props: ["todos"]
    }
</script>

<style scoped>
    
</style>

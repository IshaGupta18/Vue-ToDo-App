<template>
    <div>
        <!-- v-for is the directive for looping over a list, have a key attached to it -->
        <div v-bind:key="item.id" v-for="item in todos"> 
            <!-- we are trying to send this event up the order where we actually want the effect to take place ie App.vue has the list of todos from where we want to delete -->
            <TodoItem v-bind:todoItem="item" v-on:del-todo="$emit('del-todo', item.id)" />
        </div>
    </div>
</template>
<script>
import TodoItem from './TodoItem';
export default {
    name: "Todos",
    components: {
        TodoItem
    },
    props: ["todos"] // accepting the incoming variable todos as props
}
</script>
<style scoped>

</style>
<template>
    <!-- binding the class on the conditional -->
    <div class="todo-item" v-bind:class="{'is-complete': todoItem.completed }">
        <p>
            <!-- v-on binding an event, change is the event type, call function  markToDoComplete-->
            <input type="checkbox" v-on:change="markToDoComplete">
            {{ todoItem.title }}
            <!-- emit is for emitting the function upwards -->
            <button @click="$emit('del-todo', todoItem.id)" class="del">x</button>
        </p>
    </div>
</template>
<script>
export default {
    name: "TodoItem",
    props: ["todoItem"],
    methods: {
        markToDoComplete() {
            this.todoItem.completed = !this.todoItem.completed;
        }
    },
}
</script>
<style scoped>
  .todo-item {
    background: #f4f4f4;
    padding: 10px;
    border-bottom: 1px #ccc dotted;
  }
  .is-complete {
    text-decoration: line-through;
  }
  .del {
    background: #ff0000;
    color: #fff;
    border: none;
    padding: 5px 9px;
    border-radius: 50%;
    cursor: pointer;
    float: right;
  }
</style>
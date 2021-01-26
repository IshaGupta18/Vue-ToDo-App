<template>
  <div id="app">
    <Header />
    <AddToDo v-on:add-todo="addNewTodoF"/>
    <!-- v-bind:variableNameInComponent = dataNameInProps -->
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTODO" /> 
  </div>
</template>

<script>
// Accessing to-dos from multiple components, every item in the to-do list will have itws own component. In the add to-do form, we'll need to add those to-dos to the form
import Todos from '../components/Todos';
import AddToDo from '../components/AddNewToDo';
import axios from 'axios';
export default {
  name: 'Home',
  components: {
    Todos, AddToDo
  },
  data() {
    return {
      // todos is an array of objects
      todos: []
    }
  },
  methods: {
    deleteTODO(id) {
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      .then(this.todos = this.todos.filter(item => item.id != id))
      .catch(err => console.log(err));
      
    },
    addNewTodoF(newItem) {
      const { title, completed } = newItem;
      axios.post('https://jsonplaceholder.typicode.com/todos', {
        title, 
        completed
      })
      .then(res => this.todos = [...this.todos, res.data])
      .catch(err => console.log(err));
    },
  },
  // like componentDidMount - fired off when this component is created
  created() {
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=8')
      .then(res => this.todos = res.data)
      .catch(err => console.log(err));
  }
}
</script>

<style>
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }
  body {
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
  }
  .btn {
    display: inline-block;
    border: none;
    background: #555;
    color: #fff;
    padding: 7px 20px;
    cursor: pointer;
  }
  .btn:hover {
    background: #666;
  }
</style>

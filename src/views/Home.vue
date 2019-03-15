<template>
  <div id="app">
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />  <!-- v-bind is passing todos data array as props to the Todos component. v-on is listening for the del-todo event (which comes from clicking the x button in TodoItem component), and when it happens the deleteTodo method is invoked. -->
  </div>
</template>

<script> 
import Header from "../components/layout/Header";
import Todos from "../components/Todos";
import AddTodo from '../components/AddTodo';
import axios from 'axios';

export default {
  name: "home",
  components: { 
    Todos,
    AddTodo,
  },
  data() {
    return {
      todos: []
    }
  },
  methods: {
    async deleteTodo(id) {
      const res = await axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      try {
        this.todos = this.todos.filter(todo => todo.id !== id ) //returns all todos where the id does not match the id passed as an argument (the todo that was deleted)        
      }
      catch(err) {
        console.log(err)
      }
    },
    // This also works
    // deleteTodo(id) {
    //   axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
    //     .then(res => this.todos = this.todos.filter(todo => todo.id !== id ))
    //     .catch(err => console.log(err));
    // },
    async addTodo(newTodo) {
      const { title, completed } = newTodo;

      const res = await axios.post('https://jsonplaceholder.typicode.com/todos', {
        title,
        completed
      })
      try {
        this.todos = [...this.todos, res.data]        
      }
      catch(err) {
        console.log(err)
      }
    }
  },
  async created() { //this is like componentDidMount. It'll fire once the component loads
      const res = await axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5');
      try {
        this.todos = res.data;
      }
      catch (err) {
        console.log(err)
      }
    },
  // This also works:
  // created() {
    //   axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
    //     .then(res => this.todos = res.data)
    //     .catch(err => console.log(err));
    // }
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
 
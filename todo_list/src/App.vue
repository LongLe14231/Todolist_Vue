<template>
  <div id="app">
    <Header/>
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  
  </div>
</template>

<script>
  import Header from './components/layout/Header.vue';
  import Todos from './components/Todos.vue';
  import AddTodo from './components/AddTodo.vue';
  import axios from 'axios';
  
  
  export default {
    name: 'app',
    components: {
      Header,
      Todos,
      AddTodo
    },
    data() {
      return {
        todos: []
      }
    },
    methods: {
      deleteTodo(id) {
  
        axios.delete('https://jsonplaceholder.typicode.com/todos/${id}')
          // should put it up in here.then(res => )
        this.todos = this.todos.filter(todo => todo.id !== id);
  
      },
      addTodo(newTodo) {
        const {
          title,
          completed
        } = newTodo; //get these two from newTodo object
        axios.post('https://jsonplaceholder.typicode.com/todos', {
            title,
            completed
          }) //get is get by default, post is putting stuff into your post //make a post request from axios library, axios give out functions for making http request 
          .then(res => this.todos = [...this.todos, res.data]);
      }
    },
    created() {
      axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5') //you get 5 from server (Nodejs or Django API)
        .then(res => this.todos = res.data)
  
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
  
  .button:hover {
    background: #777;
  }
</style>

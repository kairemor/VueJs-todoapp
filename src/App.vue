<template>
  <div id="app">
    <Header />
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>
import Header from "./components/layout/Header";
import Todos from "./components/Todos";
import AddTodo from "./components/AddTodo";

export default {
  name: "app",
  components: {
    Header,
    AddTodo,
    Todos
  },
  data() {
    return {
      todos: []
    };
  },
  methods: {
    deleteTodo(id) {
      console.log(id);
      this.todos = this.todos.filter(todo => todo._id !== id);
    },
    addTodo(newTodo) {
      fetch("https://polytechbot.herokuapp.com/api/todos", {
        method: "post",
        headers: {
          "Content-Type": "application/json"
        },
        body: JSON.stringify(newTodo)
      })
        .then(res => {
          fetch("https://polytechbot.herokuapp.com/api/todos")
            .then(response => response.json())
            .then(res => {
              this.todos = res.data;
            });
        })
        .catch(err => console.log(err));
    }
  },
  created() {
    fetch("https://polytechbot.herokuapp.com/api/todos")
      .then(response => response.json())
      .then(res => {
        this.todos = res.data;
      });
  }
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0px;
  padding: 0px;
}
body {
  font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
  line-height: 1.5;
}
a {
  color: aliceblue;
  text-decoration: none;
}
.container {
  padding: 0 1rem;
}
.btn {
  display: inline-block;
  border: none;
  background: rgba(1, 48, 255, 0.671);
  padding: 5px, 20px;
  cursor: pointer;
}
.btn:hover {
  background: rgba(1, 48, 255);
}
</style>

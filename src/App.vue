<template>
  <div>
    <h1>Our To-Do App</h1>
    <button @click="createFormButton">Create New Todo</button>
    <Home v-if="!showCreateForm" :todos="todos" />
    <Create v-else @todoCreated="newTodoReceived" />
  </div>
</template>

<script>
import Home from "./components/Home.vue";
import Create from "./components/Create.vue";
import db from "./database/db.json";

export default {
  components: {
    Home,
    Create,
  },
  data() {
    return {
      showCreateForm: false,
      todos: [],
      newTodo: {
        name: "Something",
        time: "02:00",
        completed: false,
      },
    };
  },
  methods: {
    createFormButton(e) {
      if (this.showCreateForm) {
        this.showCreateForm = false;
        e.target.innerText = "Create New Todo";
      } else {
        this.showCreateForm = true;
        e.target.innerText = "Back to Todo List";
      }
    },
    newTodoReceived(value) {
      this.todos.push(value);
      console.log(this.todos);
    },
  },
  created() {
    this.todos = db;
  },
};
</script>

<style>
body {
  font-family: Arial, Helvetica, sans-serif;
  width: 70%;
  margin: 0 auto;
}
</style>

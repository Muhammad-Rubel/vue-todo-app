<template>
  <div>
    <h2>Below is the list of todo's</h2>
    <ul>
      <li v-for="(todo, index) in initialTodos" :key="index">
        <h3>{{ todo.name }}</h3>
        <p>
          Complete within <strong>{{ todo.time }}</strong>
        </p>
        <p>
          Completion Status:
          <span :class="todo.completed ? 'completed' : 'pending'">{{
            todo.completed ? "Completed" : "Pending"
          }}</span>
        </p>
        <button v-if="!todo.completed" @click="changeTodoStatus(index)">
          Done
        </button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Home",
  props: {
    todos: Array,
  },
  data() {
    return {};
  },
  methods: {
    changeTodoStatus(index) {
      this.todos[index].completed = true;
    },
  },
  computed: {
    initialTodos() {
      return this.todos;
    },
  },
};
</script>

<style>
.completed {
  font-weight: bold;
  color: darkgreen;
}

.pending {
  font-weight: bold;
  color: red;
}
</style>

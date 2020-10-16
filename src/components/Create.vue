<template>
  <div>
    <h2>Create New Todo</h2>
    <form>
      <div>
        <label for="todoName">Enter your todo Name: </label>
        <input id="todoName" name="todoName" type="text" v-model="todo.name" />
      </div>
      <div>
        <label for="todoTime">Enter your todo Time: </label>
        <select name="todoTime" id="todoTime" v-model="todo.time">
          <option v-for="time in timeArray" :key="time" :value="time">{{
            time
          }}</option>
        </select>
      </div>
      <button type="submit" @click.prevent="addTodo" :disabled="!checkForm">
        Create Todo
      </button>
    </form>
  </div>
</template>

<script>
export default {
  name: "Create",
  data() {
    return {
      todo: {
        name: "",
        time: "",
        completed: false,
      },
    };
  },
  methods: {
    addTodo() {
      this.$emit("todoCreated", this.todo);
      const todo = {
        name: "",
        time: "",
        completed: false,
      };
      this.todo = todo;
    },
  },
  computed: {
    timeArray() {
      const timeArray = [];
      for (let i = 0; i < 24; i++) {
        let t = "";
        if (i < 10) {
          t = "0";
        } else {
          t = "";
        }
        timeArray.push(`${t}${i}:00`);
      }
      return timeArray;
    },
    checkForm() {
      if (this.todo.name && this.todo.time) {
        return true;
      } else {
        return false;
      }
    },
  },
};
</script>

<style scopped>
div {
  margin-bottom: 1em;
}

select,
input {
  padding: 0.3em;
}
</style>

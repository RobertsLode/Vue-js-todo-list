<template>
  <div class="home">
    <h1>Planner</h1>
    <br />
    <input type="text" v-model="inputValue" />
    <button @click="addTask()">Add to list!</button>
  </div>
  <ol>
    <li v-for="(todo, index) in todos" :key="index">
      <input
        type="checkbox"
        @click="isCompleted(index)"
        :checked="todo.isCompleted"
      />
      <span :class="{ line: todo.isCompleted }">{{ todo.text }}</span>

      <button @click="removeTask(index)">x</button>
    </li>
  </ol>
  <button @click="filterCompleted()">Completed</button>
  <button @click="filterNotCompleted()">In progess</button>
  <button @click="filterAll()">All</button>
</template>

<style lang="scss">
@import "../styles/todo.scss";
</style>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "HomeView",
  data: () => ({
    inputValue: "",
    todos: [] as {
      text: string;
      isCompleted: boolean;
    }[],
    todosClone: [] as {
      text: string;
      isCompleted: boolean;
    }[],
  }),
  methods: {
    addTask() {
      if (this.inputValue) {
        this.todosClone.push({
          text: this.inputValue,
          isCompleted: false,
        });
        this.todos.push({
          text: this.inputValue,
          isCompleted: false,
        });
      }
      this.inputValue = "";
    },
    removeTask(index: number) {
      this.todosClone.splice(index, 1);
      this.todos.splice(index, 1);
    },
    isCompleted(index: number) {
      if (this.todos[index]) {
        this.todos[index].isCompleted = !this.todos[index].isCompleted;
      }
    },
    filterCompleted() {
      let a = this.todosClone.filter((todo) => todo.isCompleted);
      this.todos = a;
    },
    filterNotCompleted() {
      let a = this.todosClone.filter((todo) => !todo.isCompleted);
      this.todos = a;
    },
    filterAll() {
      console.log(this.todosClone);
      let a = this.todosClone.filter((todo) => todo);
      this.todos = a;
      console.log(this.todosClone);
    },
  },
});
</script>

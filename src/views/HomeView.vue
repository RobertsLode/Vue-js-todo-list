<template>
  <div class="home">
    <div class="planner--box">
      <h1>Planner</h1>
      <br />
      <div class="input--and-button">
        <form @submit.prevent action="">
          <input type="text" v-model="inputValue" />
          <button @click="addTask()">Add to list!</button>
        </form>
      </div>
      <div class="list--box">
        <div class="list--box-child">
          <div
            class="list--box-child-li"
            v-for="todo in filtered"
            :key="todo.id"
          >
            <div class="checkbox--and-todo">
              <input
                type="checkbox"
                @click="isCompleted(todo.id)"
                :checked="todo.isCompleted"
              />
              <div class="text" :class="{ line: todo.isCompleted }">
                {{ todo.text }}
              </div>
            </div>
            <button class="li--button" @click="removeTask(todo.id)">X</button>
          </div>
        </div>
      </div>
    </div>
  </div>
  <button @click="filter = 'all'">All</button>
  <button @click="filter = 'inProgress'">In progess</button>
  <button @click="filter = 'completed'">Completed</button>
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
      id: number;
    }[],

    id: 0,
    filter: "all" as "all" | "inProgress" | "completed",
  }),

  computed: {
    filtered() {
      if (this.filter === "all") {
        return this.todos;
      } else if (this.filter === "inProgress") {
        return this.todos.filter((todo) => !todo.isCompleted);
      } else if (this.filter === "completed") {
        return this.todos.filter((todo) => todo.isCompleted);
      }
      return this.todos;
    },
  },

  methods: {
    addTask() {
      if (this.inputValue) {
        this.todos.push({
          text: this.inputValue,
          isCompleted: false,
          id: this.id++,
        });
      }

      this.inputValue = "";
    },

    removeTask(index: number) {
      this.todos = this.todos.filter((todo) => todo.id !== index);
    },

    isCompleted(id: number) {
      const index = this.todos.findIndex((todo) => {
        return id === todo.id;
      });
      this.todos[index].isCompleted = !this.todos[index].isCompleted;
    },
  },
});
</script>

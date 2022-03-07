<script setup>
import { ref } from "vue";

const todoText = ref("");
const todoList = ref([]);
function add() {
  const tmp = { task: todoText.value, completed: false };
  todoList.value.push(tmp);
  todoText.value = "";
}
function toggleTask(clickIndex) {
  todoList.value = todoList.value.map((item, index) => {
    if (clickIndex === index) {
      item.completed = !item.completed;
    }
    return item;
  });
}

function removeTask(clickIndex) {
  todoList.value = todoList.value.filter((item, index) => {
    if (clickIndex === index) {
      return false;
    }
    return true;
  });
}
</script>

<template>
  <div class="content">
    <h1>Todo</h1>

    <form @submit.prevent="add()">
      <input v-model="todoText" name="todoText" autocomplete="off" />
      <button>Add</button>
    </form>
    <hr>
    <ul>
      <li
        v-for="(todo, index) in todoList"
        :key="index"
        :class="{ done: todo.completed }"
      >
        <input
          @click="toggleTask(index)"
          type="checkbox"
          id="checkbox"
          v-model="todo.completed"
        />

        <span>{{ todo.task }}</span>

        <button @click="removeTask(index)">X</button>
      </li>
    </ul>
  </div>
</template>

<style>
.content {
  width: 600px;
  margin: 0 auto;

}
form {
  display: flex;
  justify-content: space-around;
}
form input {
  width: 70%;
}
ul {
  list-style-type: none;
  padding-inline-start: 0;
}

li {
  display: flex;
  justify-content: space-between;
}

.done span {
  text-decoration: line-through;
}
</style>

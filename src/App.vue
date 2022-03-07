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
  <video autoplay muted loop id="myVideo">
    <source src="video_img/video.mp4" type="video/mp4" />
    Your browser does not support HTML5 video.
  </video>

  <div class="content">
    <h1>Todo</h1>

    <form @submit.prevent="add()">
      <input v-model="todoText" name="todoText" autocomplete="off" />
      <button>Add</button>
    </form>

    <ul>
      <li
        v-for="(todo, index) in todoList"
        :key="index"
        :class="{ completed: todo.completed }"
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
  position: fixed;
  right: 0px;
  top: 0px;
  bottom: 0px;
  width: 400px;
  /*-webkit-box-shadow: 0px 0px 45px -3px rgba(84, 92, 91, 0.44);
  -moz-box-shadow: 0px 0px 45px -3px rgba(84, 92, 91, 0.44);
  box-shadow: 0px 0px 45px -3px rgba(84, 92, 91, 0.44);*/
  background-color: rgba(94, 94, 94, 0.507);
  z-index: 100;
  padding: 1em;
  margin: 1em;
  border: 2px solid white;
}

.content h1 {
  text-align: center;
  color: white;
}
#myVideo {
  position: fixed;
  display: block;
  right: 0;
  bottom: 0;
  min-width: 100%;
  min-height: 100%;
  object-fit: contain;

  z-index: 1;
  filter: blur(1px);
  -webkit-filter: blur(1px);
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

.completed span {
  text-decoration: line-through;
}
</style>

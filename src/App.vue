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

function removeAllTask(clickIndex) {
  todoList.value = [];
}
</script>

<template>
  <div class="box">
    <video autoplay muted loop id="myVideo">
      <source src="/video_img/video.mp4" type="video/mp4" />
      Your browser does not support HTML5 video.
    </video>
  </div>

  <div class="content">
    <h1>Tasks for today</h1>
    <form @submit.prevent="add()">
      <input v-model="todoText" name="todoText" autocomplete="off" />
      <button class="add">+</button>
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
          class="largerCheckbox"
          v-model="todo.completed"
        />

        <span>{{ todo.task }}</span>

        <button @click="removeTask(index)" class="removeTask">-</button>
      </li>
    </ul>

    <button @click="removeAllTask" class="removeAll">Clean All</button>
  </div>
</template>





<style>
body {
  margin: 0;
}
.box {
  width: 100%;
  height: 100%;
}
#myVideo {
  position: fixed;
  display: block;
  min-width: 100%;
  min-height: 100%;
  object-fit: contain;
  z-index: 1;
  /*filter: blur(1px);
  -webkit-filter: blur(3px);*/
}
.content {
  position: fixed;
  display: block;
  right: 0px;
  top: 0px;
  bottom: 0px;
  width: 40%;
  -webkit-box-shadow: 0px 0px 45px -3px rgba(84, 92, 91, 0.44);
  -moz-box-shadow: 0px 0px 45px -3px rgba(84, 92, 91, 0.44);
  box-shadow: 0px 0px 45px -3px rgba(84, 92, 91, 0.44);
  background-color: rgba(255, 255, 255, 0.317);
  z-index: 100;
  padding: 1em;
  backdrop-filter: blur(2px);
}

.content h1 {
  text-align: center;
  color: 3400ee;
  font-family: Arial, Helvetica, sans-serif;
  text-transform: uppercase;
  font-size: x-large;
}

form {
  display: flex;
  justify-content: space-between;
  font-family: "Gill Sans", sans-serif;
}

input.largerCheckbox {
  transform: scale(2);
}

form input {
  width: 85%;
  border-radius: 10px;
  height: 2em;
  font-family: "Gill Sans", sans-serif;
  text-transform: uppercase;
  border-style: none;
  border: 1px solid rgba(0, 0, 0, 0.481);
}
.add {
  width: 7%;
  border-radius: 60px;
  background-color: rgba(254, 232, 66, 0.735);
  border: 1px solid gray;
  padding: 0;
  cursor: pointer;
}

.removeTask {
  width: 4%;
  border-radius: 60px;
  background-color: rgba(66, 226, 254, 0.735);
  border: 1px solid gray;
  padding: 0;
  transform: scale(1.5);
  cursor: pointer;
}

.removeAll {
  border-radius: 10px;
  border: none;
  padding: 0.5em 3em;
  bottom: 0;
  text-align: center;
  display: block;
  width: 20%;
  text-align: center;
  font-size: small;
  position: relative;
  margin: auto;
  margin-top: 10em;
  box-shadow: 0px 4px 3px 0px rgb(79, 79, 79);
  cursor: pointer;
  padding-left: 0px;
  padding-right: 0;
}
.removeAll:hover {
  background-color: #d16753;
}

.removeAll:active {
  background-color: #340e0e;
  box-shadow: 0 5px #666;
  transform: translateY(4px);
  color: white;
}

ul {
  list-style-type: none;
  padding-inline-start: 0;
}

li {
  display: flex;
  justify-content: space-between;
  font-family: "Gill Sans", sans-serif;
  text-transform: uppercase;
  align-items: center;
  line-height: 2em;
}

.completed span {
  text-decoration: line-through;
  color: gray;
}
</style>

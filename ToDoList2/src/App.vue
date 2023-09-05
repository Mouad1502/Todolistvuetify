<script setup>
import { ref } from 'vue';
const task = ref('');
const checkedList = ref([]);
const tasksList = ref([]);
const addTask = (x) => {
  tasksList.value.push(x);
  task.value="";
  return tasksList;
}
const checkTask = (x) => {
  const index = tasksList.value.indexOf(x);
  if (index !== -1) {
    checkedList.value.push(tasksList.value[index]);
    tasksList.value.splice(index, 1);
  }
}

const uncheckTask = (x) => {
  const index = checkedList.value.indexOf(x);
  if (index !== -1) {
    tasksList.value.push(checkedList.value[index]);
    checkedList.value.splice(index, 1);
  }
}
const deleteTask = (taskId) => {
  const taskIndexInTasksList = tasksList.value.findIndex((task) => task.id === taskId);
  if (taskIndexInTasksList !== -1) {
    tasksList.value.splice(taskIndexInTasksList, 1);
  }

  const taskIndexInCheckedList = checkedList.value.findIndex((task) => task.id === taskId);
  if (taskIndexInCheckedList !== -1) {
    checkedList.value.splice(taskIndexInCheckedList, 1);
  }
}
</script>

<template>
  <div class="container min-w-full min-h-screen bg-gradient-to-r from-blue-900 to-violet-800 p-2">
    <div class="todo-app w-full max-w-xl bg-white mt-24 mx-auto mb-5 pt-10 px-7 pb-16 rounded-lg">
      <h2 class="text-blue-950 text-2xl font-bold flex items-center mb-5">To-Do List<img class="w-7 ml-2" src="./images/icon.png"></h2>
      <div class="row flex items-center justify-between bg-slate-200 rounded-3xl pl-5 mb-6">
        <input type="text" id="input-box" placeholder="Add Your task" class="flex-1 border-0 outline-none bg-transparent p-2" v-model="task">
        <button @click=addTask(task) class="border-0 outline-none py-4 px-12 bg-red-600 text-white cursor-pointer rounded-full">Add</button>
      </div>
      <ul id="list-container">
          <li class="flex flex-row justify-between m-3 pt-3 pr-2 pb-3 pl-12 select-none cursor-pointer relative before:content-[''] before:absolute before:h-7 before:w-7 before:rounded-lg before:bg-[url('./src/images/unchecked.png')] before:bg-cover before:bg-center before:top-3 before:left-2" @click="checkTask(task)" v-for="task in tasksList" :key="task.id">{{ task }}<button><img src="./images/delete-button.png" class="w-8 h-8 top-3 left-2 hover:bg-black rounded-full" @click.stop="deleteTask(task.id)"></button>
          </li>
          <li class="flex flex-row justify-between m-3 check pt-3 pr-2 pb-3 pl-12 select-none cursor-pointer relative before:content-[''] before:absolute before:h-7 before:w-7 before:rounded-lg before:bg-[url('./src/images/checked.png')] before:bg-cover before:bg-center before:top-3 before:left-2 line-through" v-for="task in checkedList" :key="task.id" @click="uncheckTask(task)">{{ task }}<button><img src="./images/delete-button.png" class="w-8 h-8 top-3 left-2 hover:bg-black rounded-full" @click.stop="deleteTask(task.id)"></button>
          </li>
      </ul>
    </div>
  </div>
</template>


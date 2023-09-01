<script setup>
import { provide, ref, watchEffect } from 'vue';
import TaskViewer from './components/TaskViewer.vue';
import ToDoInput from './components/ToDoInput.vue';
import { priorityValues } from './utils/constants';

const tasks = ref(JSON.parse(localStorage.getItem('tasks')) ?? {
  id: 0, items: []
});

watchEffect(() => {
  localStorage.setItem('tasks', JSON.stringify(tasks.value));
});

const addTask = (task) => {
  if (task.title && priorityValues.includes(task.priority)) {
    tasks.value.items.unshift({ ...task, id: tasks.value.id++ });
  }
};

const toggleDisabledTask = (taskId) => {
  const taskIndex = tasks.value.items.findIndex((task) => task.id === taskId);
  if (taskIndex !== -1) {
    const task = tasks.value.items[taskIndex];
    task.disabled = !task.disabled;
  }
}
provide('toggleDisabledTask', toggleDisabledTask);

const removeTask = (taskId) => {
  const taskIndex = tasks.value.items.findIndex((task) => task.id === taskId);
  if (taskIndex !== -1) {
    tasks.value.items.splice(taskIndex, 1);
  }
}
provide('removeTask', removeTask);

</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="64"
      height="64" />
  </header>
  <main>
    <ToDoInput @add-task="addTask" />
    <TaskViewer :tasks="tasks" />
  </main>
</template>

<style scoped>
header {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>

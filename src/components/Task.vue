<script setup>
import { computed, inject } from 'vue';

const props = defineProps({ task: Object });

const toggleDisabledTask = inject('toggleDisabledTask');
const removeTask = inject('removeTask');

const classObj = computed(() => ([
  `border-${props.task.priority}`,
  { 'task-disabled': props.task.disabled ?? false }
]))

</script>

<template>
  <div class="task" :class="classObj" @click="toggleDisabledTask(task.id)">
    <p>
      {{ task.title }}
    </p>
    <button class="close-btn" @click.stop="removeTask(task.id)">&#10006;</button>
  </div>
</template>

<style scoped>
.task {
  display: flex;
  justify-content: space-between;
  width: 100%;
  padding: 1em;
  border-radius: 10px;
  background-color: var(--color-task);
  cursor: pointer;
  transition: opacity 0.3s ease;
}

.task:hover:not(.task-disabled):not(.fade-in-leave-active) {
  opacity: 0.8;
}

.task p {
  overflow-wrap: break-word;
  min-width: 0;
}

.task-disabled {
  opacity: 0.5;
}

.task-disabled:hover:not(.fade-in-leave-active) {
  opacity: 0.6;
}

.task-disabled p {
  text-decoration: line-through;
}

.border-low {
  border-left: 10px solid grey;
}

.border-medium {
  border-left: 10px solid goldenrod;
}

.border-high {
  border-left: 10px solid crimson;
}

.close-btn {
  background-color: transparent;
  border: none;
  color: var(--color-text);
  font-size: 18px;
  font-weight: bold;
  cursor: pointer;
  transition: color 0.3s ease;
}

.close-btn:hover {
  color: var(--color-text-bright);
}
</style>
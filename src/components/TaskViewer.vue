<script setup>
import { computed } from 'vue';
import Task from './Task.vue';

const props = defineProps({ tasks: Object });

const hasTasks = computed(() => props.tasks.items.length > 0);

</script>

<template>
  <div class="wrapper">
    <div v-if="!hasTasks">
      <p class="empty-message">
        Add a new task!
      </p>
    </div>
    <TransitionGroup name="fade-in" tag="div" class="task-list">
      <Task v-for="task in tasks.items" :task="task" :key="task.id"></Task>
    </TransitionGroup>
  </div>
</template>

<style scoped>
.wrapper {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 2em 0;
}

.empty-message {
  font-size: 18px;
}

.task-list {
  display: flex;
  position: relative;
  flex-direction: column;
  width: 100%;
  gap: 1em;
}

.fade-in-move,
.fade-in-enter-active,
.fade-in-leave-active {
  transition: all 0.3s ease;
}

.fade-in-enter-from,
.fade-in-leave-to {
  opacity: 0;
  transform: translateX(15%);
}

@media (min-width: 1024px) {
  .task-list {
    width: 50%;
  }
}
</style>
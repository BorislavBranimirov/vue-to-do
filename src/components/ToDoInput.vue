<script setup>
import { ref } from 'vue';
import { priorityEnum } from '../utils/constants.js';

const emit = defineEmits(['addTask']);

const title = ref('');

const selectedPriority = ref(priorityEnum[0].value ?? '');

const onSubmit = () => {
  emit('addTask', {
    title: title.value,
    priority: selectedPriority.value,
    disabled: false
  });
};
</script>

<template>
  <form @submit.prevent="onSubmit">
    <div class="group">
      <label for="title">Title:</label>
      <input type="text" name="title" id="title" placeholder="Describe the task"
        v-model="title" required>
    </div>
    <div class="group">
      <label for="priority">Priority:</label>
      <select name="priority" id="priority" v-model="selectedPriority" required>
        <option disabled value="">Severity type</option>
        <option v-for="{ value, text } in priorityEnum" :value="value"
          :key="value">
          {{ text }}
        </option>
      </select>
    </div>
    <input type="submit" value="Add">
  </form>
</template>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  gap: 1em;
  margin: 1.5em 0;
}

.group {
  display: flex;
  flex-direction: column;
  gap: 0.5em;
  width: 100%;
}

label {
  color: var(--color-text-bright);
  font-size: 18px;
  flex-shrink: 0;
}

input[type="text"],
select {
  background-color: var(--color-background);
  border: 1px solid var(--color-border);
  border-radius: 4px;
  padding: 0.5em 1em;
  color: var(--color-text-bright);
  flex-grow: 1;
}

input[type="submit"] {
  background-color: var(--color-background-soft);
  border: 1px solid var(--color-border);
  border-radius: 4px;
  padding: 0.5em 2em;
  margin-top: 1em;
  color: var(--color-text-bright);
  transition: background-color 0.3s ease;
}

input[type="submit"]:hover {
  background-color: var(--color-background-mute);
}

@media (min-width: 1024px) {
  form {
    flex-direction: row;
    align-items: center;
    gap: 1.5em;
  }

  .group {
    flex-direction: row;
    align-items: center;
    gap: 1em;
  }

  input[type="submit"] {
    margin-top: 0;
  }
}
</style>
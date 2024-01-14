<script lang="ts" setup>
import { ref } from "vue";

export type TaskCreateProps = {
  onCreateBtnClick: (taskName: string, taskDescription: string) => void;
};
defineProps<TaskCreateProps>();

const taskName = ref("");
const taskDescription = ref("");
</script>

<template>
  <form>
    <label>
      Task Name
      <input v-model="taskName" maxlength="20" type="text" />
    </label>

    <label>
      Task Description
      <textarea v-model="taskDescription" maxlength="25" />
    </label>

    <button
      @click="
        (event) => {
          event.preventDefault();
          onCreateBtnClick(taskName, taskDescription);
        }
      "
    >
      Create
    </button>
  </form>
</template>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  padding: 1.25rem;
  border-radius: 0.5rem;
  background-color: #343434;
}
</style>

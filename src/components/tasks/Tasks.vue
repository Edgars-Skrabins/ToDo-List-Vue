<script lang="ts" setup>
import TaskCreate from "./TaskCreate.vue";
import Task, { TaskProps } from "../Task.vue";
import { ref } from "vue";

const tasks = ref<TaskProps[]>([]);
const handleCreateTask = (taskName: string, taskDescription: string) => {
  if (taskName && taskDescription) {
    createTask(taskName, taskDescription);
  }
};

const createTask = (taskName: string, taskDescription: string) => {
  const newTask: TaskProps = {
    taskName: taskName,
    taskDescription: taskDescription,
  };
  tasks.value.push(newTask);
};
</script>

<template>
  <main>
    <TaskCreate :onCreateBtnClick="handleCreateTask" />
    <div v-for="(task, index) in tasks" :key="index" class="tasks">
      <Task :taskDescription="task.taskDescription" :taskName="task.taskName" />
    </div>
  </main>
</template>

<style scoped>
main {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 1rem;
}

.tasks {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}
</style>

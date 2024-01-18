<script lang="ts" setup>
import TaskCreate from "./TaskCreate.vue";
import Task, {TaskProps} from "./Task.vue";
import {onMounted, ref} from "vue";
import {deleteTaskById, getAllTasks, postTask} from "../../utils/api.ts";

const tasks = ref<TaskProps[]>([]);

const initialize = () => {
  getAllTasks()
      .then((response) => {
        tasks.value = response.data;
      })
      .catch((error) => {
        console.error(error);
      })
}

onMounted(() => {
  initialize();
})

const handleCreateTask = (taskName: string, taskDescription: string) => {
  if (taskName && taskDescription) {
    createTask(taskName, taskDescription);
  }
};

const createTask = (taskName: string, taskDescription: string) => {
  const newTask: TaskProps = {
    id: Math.random().toString(),
    taskName: taskName,
    taskDescription: taskDescription,
    onHandleDeleteBtnClick: deleteTask,
  };
  tasks.value.push(newTask);
  postTask(newTask);
};

const deleteTask = (taskId: string) => {
  tasks.value = tasks.value.filter((element) => element.id !== taskId);
  deleteTaskById(Number(taskId));
}

</script>

<template>
  <main>
    <TaskCreate :onCreateBtnClick="handleCreateTask"/>
    <div class="tasks">
      <div v-for="(task, index) in tasks" :key="index">
        <Task
            :taskDescription="task.taskDescription"
            :taskName="task.taskName"
            :on-handle-delete-btn-click="deleteTask"
            :id="task.id"
        />
      </div>
    </div>
  </main>
</template>

<style scoped>
main {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100%;
  gap: 1rem;
}

.tasks {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: row;
  flex-wrap: wrap;
  width: 100%;
  gap: 1rem;
}
</style>

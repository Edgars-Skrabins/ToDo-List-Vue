<script lang="ts" setup>
export type TaskProps = {
  id: string,
  taskName: string;
  taskDescription: string;
  onHandleDeleteBtnClick: (taskId: string) => void,
};
defineProps<TaskProps>();

const handleEditBtnClick = () => {
  console.log("Attempted edit");
};
</script>

<template>
  <main class="task" key={{id}}>
    <p>{{ taskName }}</p>
    <p>
      {{ taskDescription }}
    </p>

    <div class="buttonWrapper">
      <button @click="() => onHandleDeleteBtnClick(id)">Delete</button>
      <button @click="handleEditBtnClick">Edit</button>
    </div>
  </main>
</template>

<style scoped>
.task {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 0.25rem;
  background-color: #313131;
  border-radius: 1rem;
  padding: 1rem;
  width: 15rem;
  height: 12rem;
}

p {
  margin: 0;
}

.buttonWrapper {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  margin-top: auto;
  width: 100%;
}
</style>

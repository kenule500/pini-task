<template>
  <form @submit.prevent="handleSuubmit">
    <input type="text" placeholder="I need to..." v-model="newTask" />

    <button>Add</button>
  </form>
</template>

<script setup>
import { ref } from "vue";
import { useTaskStore } from "../stores/TaskStore";

const taskStore = useTaskStore();
const newTask = ref("");

const handleSuubmit = () => {
  if (newTask.value.length > 0) {
    taskStore.addTask({
      title: newTask.value,
      isFav: false,
      id: Math.floor(Math.random() * 10000),
    });
    newTask.value = "";
  }
};
</script>

<style lang="scss" scoped></style>

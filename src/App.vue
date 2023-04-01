<template>
  <main>
    <header>
      <img src="./assets/pinia-logo.svg" alt="pinia logo" />
      <h1>Pinia task</h1>
    </header>

    <!-- new task form  -->
    <div class="new-task-form">
      <Taskform />
    </div>
    <!-- filter  -->
    <nav class="filter">
      <button @click="filter = 'all'">All tasks</button>
      <button @click="filter = 'favs'">Fav tasks</button>
    </nav>

    <!-- loading  -->
    <div class="loading" v-if="isLoading">loading tasks...</div>
    <!-- task list  -->
    <div class="task-list">
      <div v-if="filter === 'all'">
        <p>You have {{ totalCount }} tasks left to do</p>
        <div v-for="task in tasks">
          <TaskDetails :task="task" />
        </div>
      </div>

      <div v-if="filter === 'favs'">
        <p>You have {{ favCount }} favs left to do</p>
        <div v-for="task in favs">
          <TaskDetails :task="task" />
        </div>
      </div>
    </div>

    <button @click="taskStore.$reset">reset state</button>
  </main>
</template>

<script setup>
import { useTaskStore } from "./stores/TaskStore";
import TaskDetails from "./components/TaskDetails.vue";
import { ref } from "vue";
import Taskform from "./components/Taskform.vue";
import { storeToRefs } from "pinia";

const taskStore = useTaskStore();
const filter = ref("all");
const { tasks, isLoading, favs, favCount, totalCount } = storeToRefs(taskStore);

taskStore.getTasks();
</script>

<style lang="css" scoped></style>

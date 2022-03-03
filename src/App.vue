<script setup>
import TaskCell from "./components/TaskCell.vue";
</script>

<template>
  <div class="container bg-primary-600 rounded-sm m-10 shadow-2xl">
    <div class="p-4">
      <div>
        <p class="headline-2 my-5">Todo in Vue</p>
        <form>
          <div>
            <!-- <label for="task-input" class="label-lg my-4 col">New Task:</label> -->
            <input
              id="task-input"
              class="input input-lg mt-3 mb-5"
              placeholder="Please add new task"
              required="true"
              type="text"
            />
            <button class="m-5 btn success p-5" type="submit">Add +</button>
          </div>
        </form>
      </div>
      <div class="py-10 px-5">
        <TaskCell />

        <TaskCell />

        <TaskCell />

        <TaskCell />
      </div>
    </div>
  </div>
</template>

<style>
@import "./assets/base.css";
</style>

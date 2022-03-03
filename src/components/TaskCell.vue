<script setup>
defineProps({
  task_info: {
    type: String,
    required: true,
  },
});
</script>

<template>
  <div class="p-3 my-3 row rounded-sm bg-primary-200">
    <p class="task-info container body-lg col">Demo Task</p>
    <button class="btn primary sm col-1">Done</button>

    <button class="btn primary sm col-1">Delete</button>
  </div>
</template>

<style scoped>
.task-info {
  color: #222222;
}
</style>

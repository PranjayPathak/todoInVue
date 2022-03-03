<script>
export default {
  data() {
    return {
      task: "",
    };
  },
  props: {
    taskInfo: {
      type: Object,
      default: "default task",
      required: true,
    },
  },
  methods: {
    deleteTask() {
      this.$emit("delTask", this.task.id);
    },
  },
  mounted() {
    this.task = this.taskInfo;
  },
};
</script>

<template>
  <div>
    <div class="p-3 my-3 row rounded-sm bg-primary-200">
      <p class="task-info container body-lg col">{{ this.task.data }}</p>
      <!-- <button class="btn primary sm col-1">Done</button> -->

      <button class="btn primary sm col-1" @click="deleteTask">Delete</button>
    </div>
  </div>
</template>

<style scoped>
.task-info {
  color: #222222;
}

/* .strike {
  text-decoration: line-through;
} */
</style>

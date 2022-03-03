<script>
import TaskCell from "./components/TaskCell.vue";
export default {
  name: "App",
  data() {
    return {
      demoTasks: [
        {
          data: "demo task 1",
          id: 0,
        },
        {
          data: "demo task 2",
          id: 1,
        },
        {
          data: "demo task 3",
          id: 2,
        },
        {
          data: "demo task 4",
          id: 3,
        },
      ],
      newTask: "",
    };
  },
  methods: {
    addTask() {
      this.demoTasks.unshift({ data: this.newTask, id: this.demoTasks.length });
    },
    deleteTask(taskId) {
      let prevTasks = [...this.demoTasks];
      let newDemoTasks = prevTasks.filter((task) => {
        //filtering task that matches the description
        return task.id !== taskId;
      });
      this.demoTasks = newDemoTasks;
    },
  },
  components: { TaskCell },
};
</script>

<template>
  <div class="container bg-primary-600 rounded-sm m-10 shadow-2xl">
    <div class="p-2">
      <div class="py-5">
        <p class="headline-2 my-5">Todo in Vue</p>
        <form @submit.prevent="addTask">
          <div>
            <input
              id="task-input"
              class="input input-lg mt-3 mb-5"
              v-model="newTask"
              placeholder="Please add new task"
              required="true"
              type="text"
            />
            <button class="m-5 btn success p-5">Add +</button>
          </div>
        </form>
      </div>
      <div
        class="py-1 px-5"
        v-for="taskInfo in this.demoTasks"
        :key="taskInfo.id"
      >
        <TaskCell :task-info="taskInfo" v-on:delTask="deleteTask($event)" />
      </div>
    </div>
  </div>
</template>

<style>
@import "./assets/base.css";
</style>

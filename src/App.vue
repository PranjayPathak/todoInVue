<script>
import TaskCell from "./components/TaskCell.vue";
export default {
  name: "App",
  data() {
    return {
      demoTasks: [
        {
          data: "demo task 1",
          id: 1646702392949,
          isDone: false,
        },
      ],
      newTask: "",
    };
  },
  methods: {
    addTask() {
      let check = true; //flag to check if task already exists
      this.demoTasks.map((task) => {
        if (task.data === this.newTask) {
          check = false;
        }
      });
      if (check) {
        this.demoTasks.unshift({
          data: this.newTask,
          id: Date.now(),
        });
      }
    },
    deleteTask(taskId) {
      let prevTasks = [...this.demoTasks];
      let newDemoTasks = prevTasks.filter((task) => {
        //filtering task with same ID
        return task.id !== taskId;
      });
      this.demoTasks = newDemoTasks;
    },
    editTask(taskId) {
      console.log(taskId);
      this.demoTasks.map((task) => {
        if (task.id == taskId) {
          //remove task from list and pass to input
          this.deleteTask(taskId);
          this.newTask = task.data;
        }
      });
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
        <form v-on:submit.prevent="addTask">
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
      <div class="py-1 px-5" v-for="task in demoTasks" v-bind:key="task.id">
        <TaskCell
          v-bind:task="task"
          v-on:editTask="editTask($event)"
          v-on:delTask="deleteTask($event)"
        />
      </div>
    </div>
  </div>
</template>

<style>
@import "./assets/base.css";
</style>

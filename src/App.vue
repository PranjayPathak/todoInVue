<script>
import TaskCell from "./components/TaskCell.vue";
export default {
  name: "App",
  data() {
    return {
      demoTasks: [
        {
          data: "Sample task 1",
          id: 1646702392949,
          isCompleted: true,
        },
        {
          data: "Sample task 2",
          id: 1246702392949,
          isCompleted: true,
        },
        {
          data: "Sample task 3",
          id: 1236723921949,
          isCompleted: false,
        },
        {
          data: "Sample task 4",
          id: 1246702392149,
          isCompleted: true,
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
          isCompleted: false,
        });
        this.newTask = ""; //reset task in input
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
      this.demoTasks.map((task) => {
        if (task.id === taskId) {
          //remove task from list and pass to input
          this.deleteTask(taskId);
          this.newTask = task.data;
        }
      });
    },
    toggleStatus(taskId) {
      this.demoTasks.map((task) => {
        if (task.id === taskId) {
          task.isCompleted = !task.isCompleted;
        }
      });
    },
  },
  components: { TaskCell },
};
</script>

<template>
  <div class="todo_container bg-primary-600 rounded-sm m-10 p-5 shadow-2xl">
    <div>
      <div>
        <p class="headline-2 my-5">My Tasks</p>
        <form v-on:submit.prevent="addTask">
          <div class="form_container">
            <input
              id="task-input"
              class="input input-lg mt-3 mb-5 rounded-sm"
              v-model="newTask"
              placeholder="Please add new task"
              maxlength="50"
              required="true"
              type="text"
            />
            <button class="add_button m-5 btn success p-5">Add +</button>
          </div>
        </form>
      </div>
      <div class="p-1" v-for="task in demoTasks" v-bind:key="task.id">
        <TaskCell
          v-bind:task="task"
          v-on:editTask="editTask($event)"
          v-on:delTask="deleteTask($event)"
          v-on:toggleStatus="toggleStatus($event)"
        />
      </div>
    </div>
  </div>
</template>

<style>
@import "./assets/base.css";
.headline-2 {
  text-align: center;
}

button {
  font-weight: 600;
}

.form_container {
  display: flex;
}

.input {
  height: 4rem;
}

.add_button {
  position: absolute;
  height: 3rem;
  top: 1.2rem;
  right: 1rem;
  white-space: nowrap;
}

.todo_container {
  min-height: 90vh;
}
</style>

<script>
export default {
  data() {
    return {
      task: "",
      done: false, //checkbox input state
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
    editTask() {
      this.$emit("editTask", this.task.id);
    },
  },
  mounted() {
    this.task = this.taskInfo;
  },
};
</script>

<template>
  <div class="taskcell">
    <div class="p-3 my-3 row rounded-sm bg-primary-200">
      <p
        class="color-black container body-lg col"
        v-bind:class="{ strike: done }"
      >
        {{ this.task.data }}
      </p>
      <div class="taskcell__inputs col-4">
        <div>
          <label class="color-black" for="done">Done</label>
          <input
            type="checkbox"
            maxlength="5"
            id="done"
            value="true"
            v-model="done"
          />
        </div>
        <button
          class="btn primary sm"
          v-bind:disabled="done"
          v-on:click="editTask()"
        >
          Edit
        </button>
        <button class="btn primary sm" v-on:click="deleteTask()">Delete</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.color-black {
  color: #222222;
}

.taskcell__inputs {
  display: flex;
  flex-direction: row;
  align-items: center;
  text-align: center;
  justify-content: space-around;
}

.strike {
  text-decoration: line-through;
}
</style>

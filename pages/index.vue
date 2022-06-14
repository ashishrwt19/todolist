<template>
  <div class="mainContainer">
    <TaskAdd
      @closeModal="closeModal($event)"
      v-if="addTask == 1"
      @createTask="submitTask($event)"
    />
    <div><h1>TO-DO LIST</h1></div>
    <div class="newTaskContainer">
      <label>Add Task </label>
      <button class="add" @click="addTask = 1">+</button>
    </div>

    <div class="buttonContainer">
      <button class="pendingTaskButton" @click="currentWindow = 'Pending'">
        Pending Tasks
      </button>
      <button class="completedTaskButton" @click="currentWindow = 'Completed'">
        Completed Tasks
      </button>
    </div>

    <div class="listContainer">
      <TaskList
        v-if="currentWindow === 'Pending'"
        :isChecked="false"
        heading="Pending Tasks"
        :listItems="pendingTasks"
        @clicked="taskDone($event)"
      />
      <TaskList
        v-if="currentWindow === 'Completed'"
        heading="Completed Tasks"
        :isChecked="true"
        :listItems="completedTasks"
        @clicked="taskPending($event)"
      />
    </div>
  </div>
</template>

<script>
import TaskList from "~/components/TaskList.vue";
import TaskAdd from "../components/TaskAdd.vue";
export default {
  name: "IndexPage",

  data() {
    return {
      addTask: 0,
      currentWindow: "Pending",
      pendingTasks: [],
      completedTasks: [],
    };
  },
  updated() {
    if (this.currentWindow === "Completed") {
      this.$el.querySelectorAll(
        ".completedTaskButton"
      )[0].style.backgroundImage =
        "linear-gradient(to right, #792dd9, #ad32f9)";
      this.$el.querySelectorAll(".pendingTaskButton")[0].style.backgroundImage =
        "linear-gradient(to right bottom, #373942, #5b5a5e)";
    }
    if (this.currentWindow === "Pending") {
      this.$el.querySelectorAll(".pendingTaskButton")[0].style.backgroundImage =
        "linear-gradient(to right, #792dd9, #ad32f9)";
      this.$el.querySelectorAll(
        ".completedTaskButton"
      )[0].style.backgroundImage =
        "linear-gradient(to right bottom, #373942, #5b5a5e)";
    }
  },
  methods: {
    closeModal(item) {
      this.addTask = item;
    },
    submitTask(form) {
      console.log(form.time)
      if (form.taskTitle != "" && form.time != "Select Time") {
        this.pendingTasks.push(form);
        this.pendingTasks.sort((a, b) => (a.time > b.time ? 1 : -1));
        this.addTask = 0;
      }
      else{
        alert("Fill all the details")
      }
    },

    taskDone(item) {
      this.completedTasks.push(item);
      this.pendingTasks.splice(this.pendingTasks.indexOf(item), 1);
    },
    taskPending(item) {
      if (item.taskType == "P") {
        this.pendingTasks.push(item);
      } else {
        this.pendingTasks.unshift(item);
      }
      this.completedTasks.splice(this.completedTasks.indexOf(item), 1);
      this.pendingTasks.sort((a, b) => (a.time > b.time ? 1 : -1));
    },
  },

  components: {
    TaskList,
    TaskAdd,
  },
};
</script>

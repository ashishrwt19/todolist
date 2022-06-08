<template>
  <div class="mainContainer" >
    <TaskAdd @closeModal="addModal($event)" v-if="addTask == 1" @createTask="submitTask($event)" />
    <div><h1>TO-DO LIST</h1></div>
    <div class="newTaskContainer">
      <label>Add Task  </label>
      <button class="add" @click="(addTask = 1)">+</button>
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
    addModal(item) {
      this.addTask = item;
    },
    submitTask(form) {
        this.pendingTasks.push([form.taskTitle, false]);
        this.addTask = 0
        
    },
    taskDone(item) {
      this.completedTasks.push([item[0], true]);
      this.pendingTasks.splice(this.pendingTasks.indexOf(item), 1);
    },
    taskPending(item) {
      this.pendingTasks.push([item[0], false]);
      this.completedTasks.splice(this.completedTasks.indexOf(item), 1);
    },
    // taskDelete(item) {
    //   if (this.completedTasks.includes(item)) {
    //     this.completedTasks.splice(this.completedTasks.indexOf(item), 1);
    //   } else if (this.pendingTasks.includes(item)) {
    //     this.pendingTasks.splice(this.pendingTasks.indexOf(item), 1);
    //   }
    // },
  },

  components: {
    TaskList,
    TaskAdd,
  },
};
</script>
<style>
body {
  height: 100vh;
  background-image: linear-gradient(to bottom, #1e1f25, #231d3f);
  font-family: "Poppins", sans-serif;
  text-align: center;
  margin-top: 30px;
}
</style>

<style scoped>
.mainContainer {
  color: white;
  text-align: center;
}
label {
  font-size: x-large;
}
.listContainer {
  display: flex;
  justify-content: space-around;
}
.newTaskContainer {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 10px;
  height: 50px;
}
.inputTextField {
  border-radius: 4px 0 0 4px;
  padding: 0 10px;
  background-color: #303545;
  color: white;
  font-size: larger;
  margin: 10px 0;
  min-width: 400px;
  border: none;
  height: 100%;
}

.add {
  margin-left: 20px;
  border-radius: 50%;
  border: none;
  color: white;
  font-size: larger;
  width: 50px;
  cursor: pointer;
  background-image: linear-gradient(to right, #792dd9, #ad32f9);
  height: 100%;
}
.completedTaskButton {
  border-radius: 4px;
  border: none;
  color: white;
  font-size: larger;
  width: 150px;
  background-image: linear-gradient(to right bottom, #373942, #5b5a5e);
  cursor: pointer;
  height: 50px;
  margin: 10px;
  background-color: #25262a;
}
.pendingTaskButton {
  border-radius: 4px;
  border: none;
  background-image: linear-gradient(to right, #792dd9, #ad32f9);
  color: white;
  font-size: larger;
  width: 150px;
  cursor: pointer;
  height: 50px;
  margin: 10px;
  /* background-color: #25262a; */
}

.completedTaskButton:focus {
  background-image: linear-gradient(to right, #792dd9, #ad32f9);
}
.pendingTaskButton:focus {
  background-image: linear-gradient(to right, #792dd9, #ad32f9);
}
.buttonContainer {
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
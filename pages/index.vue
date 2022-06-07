<template>
  <div class="mainContainer">
    <div><h1>TO-DO LIST</h1></div>
    <label>Add Task</label>
    <div class="newTaskContainer">
      <input class="inputTextField" @keyup.enter="submitTask" type="text" />
      <button @click="submitTask">+</button>
    </div>
    <div class="listContainer">
      <TaskList
        :isChecked="false"
        heading="Pending Tasks"
        :listItems="pendingTasks"
        @clicked="taskDone($event)"
        @delete="taskDelete($event)"
      />
      <TaskList
        heading="Completed Tasks"
        :isChecked="true"
        :listItems="completedTasks"
        @clicked="taskPending($event)"
        @delete="taskDelete($event)"
      />
    </div>
  </div>
</template>

<script>
import TaskConfig from "~/components/TaskConfig.vue";
import TaskList from "~/components/TaskList.vue";
export default {
  name: "IndexPage",

  data() {
    return {
      pendingTasks: [],
      completedTasks: [],
    };
  },
  methods: {
    submitTask() {
      const textInput = this.$el.querySelector(".inputTextField");
      if(textInput.value){
      this.pendingTasks.push(textInput.value);
      textInput.value = "";
      }
    },
    taskDone(item) {
      this.completedTasks.push(item);
      this.pendingTasks.splice(this.pendingTasks.indexOf(item), 1);
    },
    taskPending(item) {
      this.pendingTasks.push(item);
      this.completedTasks.splice(this.completedTasks.indexOf(item), 1);
    },
    taskDelete(item) {
      if (this.completedTasks.includes(item)) {
        this.completedTasks.splice(this.completedTasks.indexOf(item), 1);
      } else if (this.pendingTasks.includes(item)) {
        this.pendingTasks.splice(this.pendingTasks.indexOf(item), 1);
      }
    },
  },

  components: {
    TaskConfig,
    TaskList,
  },
};
</script>
<style>
body {
  background-color: #25262a;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
}
</style>

<style scoped>
.mainContainer {
  color: white;
  font-family: Helvetica;
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
  margin: 20px;
  height: 50px;
}
.inputTextField {
  border-radius: 4px;
  padding: 0 10px;
  background-color: #25262a;
  color: white;
  font-size: larger;
  margin: 10px 0;
  min-width: 400px;
  border: 1px solid #ccc;
  height: 100%;
}

button {
  border-radius: 4px;
  border: 1px solid #ffffff;
  color: white;
  font-size: larger;
  width: 50px;
  cursor: pointer;
  background-color: #25262a;
  height: 109%;
}
</style>
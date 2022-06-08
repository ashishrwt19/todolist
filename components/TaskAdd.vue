<template>
  <div v-if="close == 1" class="modalOverlay">
    <div class="modalBody">
      <div>
        <i
          @click="(close = 0), $emit('closeModal', close)"
          class="bi bi-x-lg"
        ></i>
      </div>
      <div><h1>Create New Task</h1></div>
      <div>
        <input
          class="inputTextField"
          placeholder="Task Title"
          v-model="form.taskTitle"
          type="text"
        />
      </div>
      <p>Task type</p>
      <div>
        <button
          @click="
            (activeI = 'active'), (activeP = ''), (form.taskType = 'Important')
          "
          class="btnBasic"
          :class="activeI"
        >
          Important
        </button>
        <button
          @click="
            (activeP = 'active'), (activeI = ''), (form.taskType = 'Planned')
          "
          class="btnBasic"
          :class="activeP"
        > 
          Planned
        </button>
      </div>
      <p>Category</p>
      <div class="categories"></div>
      <div>
        <button
          class="createTask"
          @click="$emit('createTask', form), (close = 0)"
        >
          CREATE TASK
        </button>
      </div>
      <h2>{{ JSON.stringify(form) }}</h2>
    </div>
  </div>
</template>

<script>
export default {
  name: "TaskCofig",
  methods: {},
  emits: {
    addTask() {},
  },
  data() {
    return {
      activeI: "",
      activeP: "",
      form: {
        taskTitle: "",
        taskType: "",
      },
      close: 1,
    };
  },
  created() {},
};
</script>

<style scoped>
.modalOverlay {
  z-index: 2;
  position: fixed;
  display: flex;
  justify-content: center;
  align-items: center;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: #50505050;
}

.modalBody {
  text-align: left;
  border-radius: 10px;
  background-image: linear-gradient(to bottom right, #231e3a, #1e1f25);
  width: 500px;
  height: 500px;
  padding: 20px;
  z-index: 100;
}
.inputTextField {
  border-radius: 10px;
  padding: 15px 10px;
  background-color: #303545;
  color: white;
  font-size: larger;
  margin: 10px 0;
  width: calc(100% - 40px);
  border: none;
}

.btnBasic {
  font-family: Helvetica;
  font-weight: 600;
  cursor: pointer;
  background: transparent;
  border-radius: 4px;
  border: 2px solid #303545;
  color: #303545;
  padding: 10px;
}

.btnBasic:hover {
  background-color: #2661ef;
  color: #ffffff;
  padding: 12px;
  border: none;
}
.active {
  background-color: #2661ef;
  color: #ffffff;
  padding: 12px;
  border: none;
}
.categories {
  display: flex;
  flex-wrap: wrap;
}
.createTask {
  color: white;
  padding: 15px;
  font-family: "Poppins";
  width: 100%;
  font-weight: 600;
  text-align: center;
  border: none;
  border-radius: 4px;
  background-image: linear-gradient(to right, #792dd9, #ad32f9);
}
</style>
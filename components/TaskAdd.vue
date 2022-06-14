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
        <button @click="isImportant()" class="btnBasic" :class="activeI">
          Important
        </button>
        <button @click="isPlanned()" class="btnBasic" :class="activeP">
          Planned
        </button>
      </div>
      <div class="dateTime">
        <div class="dateTimeContainer">
          <input type="date" v-model="form.date" />
          <div class="dateTimeLayout">
            <i class="bi bi-calendar3"></i>
            {{ form.date }}
          </div>
        </div>
        <div class="dateTimeContainer">
          <input type="time" v-model="form.time" />
          <div class="dateTimeLayout">
            <i class="bi bi-clock"></i>
            {{ form.time }}
          </div>
        </div>
      </div>
      <div>
        <p>Category</p>
        <CategoryButtons
          @selectCat="addCategoryIcon($event)"
          :buttons="cButtons"
        >
        </CategoryButtons>
      </div>
      <div>
        <button class="createTask" @click="$emit('createTask', form)">
          CREATE TASK
        </button>
      </div>
      <!-- <h2>{{ JSON.stringify(form) }}</h2> -->
    </div>
  </div>
</template>

<script>
import CategoryButtons from "./CategoryButtons.vue";
export default {
  name: "TaskCofig",
  methods: {
    addCategoryIcon(button) {
      this.form.taskCategoryIcon = button.icon;
      this.form.taskCategoryColor = button.color;
    },
    isImportant() {
      this.activeI = "active";
      this.activeP = "";
      this.form.taskType = "I";
    },
    isPlanned() {
      this.activeI = "";
      this.activeP = "active";
      this.form.taskType = "P";
    },
  },
  emits: {
    addTask() {},
  },
  data() {
    return {
      cButtons: [
        {
          name: "All",
          icon: "list-ul",
          isbtn: true,
          color: "#234ebc",
        },
        {
          name: "Food",
          icon: "apple",
          isbtn: false,
          color: "#d95c5d",
        },
        {
          name: "Work",
          icon: "pc-display",
          isbtn: false,
          color: "#f29732",
        },
        {
          name: "Shopping",
          icon: "bag-fill",
          isbtn: false,
          color: "#6557ff",
        },
        {
          name: "Design",
          icon: "window-sidebar",
          isbtn: false,
          color: "#2bc8d9",
        },
      ],
      activeI: "active",
      activeP: "",
      form: {
        time: "Select Time",
        date: "Select a date",
        taskTitle: "",
        taskType: "I",
        taskCategoryColor: "#234ebc",
        taskCategoryIcon: "list-ul",
      },
      close: 1,
    };
  },
  created() {},
  components: { CategoryButtons },
};
</script>

<style scoped>
</style>
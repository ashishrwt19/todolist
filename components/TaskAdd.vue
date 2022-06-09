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
            (activeI = 'active'), (activeP = ''), (form.taskType = 'I')
          "
          class="btnBasic"
          :class="activeI"
        >
          Important
        </button>
        <button
          @click="
            (activeP = 'active'), (activeI = ''), (form.taskType = 'P')
          "
          class="btnBasic"
          :class="activeP"
        >
          Planned
        </button>
      </div>
      <p>Category</p>
      <div class="categories">
        <button
          @click="
            (form.taskCategory = 'All'),
              (form.taskCategoryIcon = 'list-ul'),
              (isFood = false),
              (isWork = false),
              (isDesign = false),
              (isShopping = false),
              (isAll = true)
          "
          class="btnCategory"
          :class="designCat"
          style="border: 2px solid #234ebc"
          :style="{ 'background-color': isAll ? '#234ebc' : 'transparent' }"
        >
          All
        </button>
        <button
          @click="
            (form.taskCategory = 'Food'),
              (form.taskCategoryIcon = 'egg-fried'),
              (isFood = true),
              (isWork = false),
              (isDesign = false),
              (isShopping = false),
              (isAll = false)
          "
          class="btnCategory"
          :class="foodCat"
          style="border: 2px solid #d95c5d"
          :style="{ 'background-color': isFood ? '#d95c5d' : 'transparent' }"
        >
          Food
        </button>
        <button
          @click="
            (form.taskCategory = 'Work'),
              (form.taskCategoryIcon = 'person-workspace'),
              (isFood = false),
              (isWork = true),
              (isDesign = false),
              (isShopping = false),
              (isAll = false)
          "
          class="btnCategory"
          :class="workCat"
          style="border: 2px solid #f29732"
          :style="{ 'background-color': isWork ? '#f29732' : 'transparent' }"
        >
          Work
        </button>
        <button
          @click="
            (form.taskCategory = 'Shopping'),
              (form.taskCategoryIcon = 'bag-fill'),
              (isFood = false),
              (isWork = false),
              (isDesign = false),
              (isShopping = true),
              (isAll = false)
          "
          class="btnCategory"
          :class="exerciseCat"
          style="border: 2px solid #6557ff"
          :style="{
            'background-color': isShopping ? '#6557ff' : 'transparent',
          }"
        >
          Shopping
        </button>
        <button
          @click="
            (form.taskCategory = 'Design'),
              (form.taskCategoryIcon = 'window-sidebar'),
              (isFood = false),
              (isWork = false),
              (isDesign = true),
              (isShopping = false),
              (isAll = false)
          "
          class="btnCategory"
          :class="designCat"
          style="border: 2px solid #2bc8d9"
          :style="{ 'background-color': isDesign ? '#2bc8d9' : 'transparent' }"
        >
          Design
        </button>
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
export default {
  name: "TaskCofig",
  methods: {},
  emits: {
    addTask() {},
  },
  data() {
    return {
      isFood: false,
      isWork: false,
      isShopping: false,
      isDesign: false,
      isAll: true,
      activeI: "active",
      activeP: "",
      form: {
        taskTitle: "",
        taskType: "I",
        taskCategory: "All",
        taskCategoryIcon: "list-ul",
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
  max-width: 500px;
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
  margin: 5px;
  cursor: pointer;
  background: transparent;
  border-radius: 4px;
  border: 2px solid #303545;
  color: #5e626c;
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
  margin-top: 30px;
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

.btnCategory {
  padding: 10px 20px;
  color: white;
  border-radius: 4px;
  border: 2px solid gray;
  margin: 5px;
  cursor: pointer;
  background-color: transparent;
}
</style>
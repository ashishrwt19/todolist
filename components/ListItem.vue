<template>
  <div class="itemContainer">
    <label class="task" @change="$emit('clicked', task)">
      <input id="checkbox" type="checkbox" :checked="task[1]" />
      <span class="checkmark"></span>
      <span class="taskText">
        <i
          :class="'bi bi-' + task[0].taskCategoryIcon"
          style="margin-right: 10px"
        ></i>
        <span>
          {{ task[0].taskTitle }}
        </span>
        <span style="margin-left: auto; color: #d95c5d;">
        {{task[0].taskType}}
        </span>
      </span>
      <!-- <button @click="$emit('delete', task)">-</button> -->
    </label>
  </div>
</template>

<script>
export default {
  name: "ListItem",
  created() {
    console.log(typeof this.isChecked);
  },
  props: {
    task: Array,
    isChecked: {
      type: Boolean,
      default: false,
    },
  },
  updated() {
    const checkbox = this.$el.querySelectorAll("#checkbox")[0];
    checkbox.checked = this.isChecked;
  },
};
</script>

<style scoped>
.task {
  position: relative;
  align-items: center;
  border-radius: 10px;
  padding: 30px 35px;
  display: flex;
  justify-content: left;
}
.taskText {
  width: 100%;
  background-color: #303545;
  align-items: center;
  border-radius: 10px;
  padding: 20px 20px;
  display: flex;
  justify-content: left;
  margin-left: 50px;
  font-size: 18px;
}
button {
  color: white;
  font-size: x-large;
  border: 1px solid white;
  background-color: #25262a;
  min-width: 40px;
  height: 40px;
  margin-left: auto;
}

.task input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}

.checkmark {
  border-radius: 5px;
  position: absolute;
  top: 50%;
  transform: translate(0, -50%);
  left: 30px;
  height: 25px;
  width: 25px;
  border: 2px solid #3d3d53;
  background-color: transparent;
}

.task:hover input ~ .checkmark {
  background-color: #3d3d53;
}

.task input:checked ~ .checkmark {
  background-color: #66ffa7;
}

.checkmark:after {
  content: "";
  position: absolute;
  display: none;
}

.task input:checked ~ .checkmark:after {
  display: block;
}

.task .checkmark:after {
  left: 9px;
  top: 5px;
  width: 5px;
  height: 10px;
  border: solid #0d4e2d;
  border-width: 0 3px 3px 0;
  -webkit-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  transform: rotate(45deg);
}
</style>
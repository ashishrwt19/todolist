<template>
  <div class="itemContainer">
    <label class="task" @change="$emit('clicked', task)">
      <input id="checkbox" type="checkbox" :checked="isChecked" />
      <span class="checkmark"></span>
      <span class="taskText">
        <div
          class="iconContainer"
          :style="{ backgroundColor: task.taskCategoryColor }"
        >
          <i :class="'bi bi-' + task.taskCategoryIcon"></i>
        </div>
        <span>
          {{ task.taskTitle }}
        </span>
        <span style="margin-left: auto; color: #d95c5d">
          {{ task.time }}
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
    task: Object,
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

<style>

</style>
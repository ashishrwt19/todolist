<template>
  <div>
    <label class="task" @change="$emit('clicked', task)">
      <input type="checkbox" :checked="isChecked" />
      <span class="checkmark"></span>
      <span>{{ task }}</span>

      <button @click="$emit('delete', task)">-</button>
    </label>
  </div>
</template>

<script>
export default {
  name: "ListItem",
  created() {
    console.log(typeof this.isChecked);
  },
  props: { task: String,
  isChecked:{ 
    type:Boolean,
    default:false  
    } },
};
</script>

<style scoped>
.task {
  position: relative;
  align-items: center;
  padding-left: 35px;
  margin: 10px;
  border-radius: 4px;
  border: 1px solid #ffffff;
  padding: 30px 35px;
  display: flex;
  justify-content: left;
}
span {
  margin: 0 10px;
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

/* Hide the browser's default checkbox */
.task input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}

/* Create a custom checkbox */
.checkmark {
  position: absolute;
  top: 50%;
  transform: translate(0, -50%);
  left: 0;
  height: 25px;
  width: 25px;
  border: 1px solid white;
  background-color: #25262a;
}

/* On mouse-over, add a grey background color */
.task:hover input ~ .checkmark {
  background-color: #35363b;
}

/* When the checkbox is checked, add a blue background */
.task input:checked ~ .checkmark {
  background-color: #25262a;
}

/* Create the checkmark/indicator (hidden when not checked) */
.checkmark:after {
  content: "";
  position: absolute;
  display: none;
}

/* Show the checkmark when checked */
.task input:checked ~ .checkmark:after {
  display: block;
}

/* Style the checkmark/indicator */
.task .checkmark:after {
  left: 9px;
  top: 5px;
  width: 5px;
  height: 10px;
  border: solid white;
  border-width: 0 3px 3px 0;
  -webkit-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  transform: rotate(45deg);
}
</style>
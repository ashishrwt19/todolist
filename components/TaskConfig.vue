<template>
  <div class="container">
    <input class="inputTextField" type="text" />
    <button>+</button>

    <!-- <div v-for="(item,i) in arrays" :key="i">
      {{item[0]}} <span style="font-size: xx-large;"> {{item[1]}}</span>
    </div> -->
  </div>
</template>

<script>
export default {
  name: "TaskCofig",
  methods: {
    onSubmit() {
      return true;
    },
  },
  emits: {
    addTask() {},
  },
  data() {
    return {
        // classes: ["Class-I", "Class-II", "Class-III"],
        // arrays: [],
    };
  },
    created() {

    //   for(var i =0; i < this.classes.length; i++) {
    //       console.log(i)
    //       this.arrays.push(this.classes[i].split("-"));
    //   };
    },
};
</script>

<style scoped>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 20px;
  height: 50px;
}
.inputTextField {
  padding: 0 10px;
  font-size: larger;
  margin: 10px;
  min-width: 400px;
  border: 1px solid #ccc;
  height: 100%;
}


button {
  border: none;
  font-size: larger;
  width: 40px;
  cursor: pointer;
  background-color: #ccc;
  height: 100%;
}
</style>
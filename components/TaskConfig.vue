<template>
  <div class="container">
    <input class="inputTextField" type="text" />
    <button>+</button>
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
    return {};
  },
  created() {},
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
  background-color: #303545;
  padding: 0 10px;
  font-size: larger;
  margin: 10px;
  min-width: 400px;
  height: 100%;
}

button {
  border: none;
  font-size: larger;
  width: 40px;
  cursor: pointer;
  height: 100%;
}
</style>
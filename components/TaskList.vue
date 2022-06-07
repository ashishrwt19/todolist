<template>
  <div class="container">
    <div>
      <h2>{{ heading }}</h2>
    </div>
    <hr>
    <div v-for="(item, i) in listItems" :key="i">
      <ListItem
        :task="item"
        @delete="handleDelete(item)"
        @clicked="handleClick(item)"
        :isChecked="isChecked"
      />
    </div>
  </div>
</template>

<script>
import ListItem from "./ListItem.vue";
export default {
  name: "TaskList",
  props: { heading: String, listItems: Array, isChecked: Boolean },
  components: { ListItem },
  methods: {
    handleClick(item) {
      this.$emit("clicked", item);
    },
    handleDelete(item){
      this.$emit("delete", item)
    }
  },
};
</script>

<style scoped>
.container {
  border-radius: 4px ;
  border: 1px solid #ccc;
  width: 500px;
  height: 500px;
  overflow: auto;
}
</style>
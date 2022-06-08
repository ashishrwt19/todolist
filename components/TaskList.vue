<template>
  <div class="container">
    <div>
      <h2>{{ heading }}</h2>
    </div>
    
    <div v-for="(item, i) in listItems" :key="i">
      <ListItem
        :task="item"
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
    // handleDelete(item){
    //   this.$emit("delete", item)
    // }
  },
};
</script>

<style scoped>
.container {
  border-radius: 10px ;
  background-image: linear-gradient(to bottom right, #332a5d, #292b33);
  width: 500px;
  height: 500px;
  overflow: auto;
}
h2{
  color: #7c47ea;
  font-weight: 800 ;

}
</style>
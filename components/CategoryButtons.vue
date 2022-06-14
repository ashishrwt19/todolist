<template>
  <div class="categoryContainer">
    <button
      class="buttonCat"   
      v-for="(button, i) in buttons"
      :key="i"
      @click="
        $emit('selectCat', button), isButton(), (button.isbtn = true)
      "
      :style="{
        borderColor: button.color,
        'background-color': button.isbtn ? button.color : 'transparent',
      }"
    >
      {{ button.name }}
    </button>
  </div>
</template>

<script>
export default {
  name: "CategoryButtons",
  data() {
    return {};
  },
  props: { buttons: Array },
  methods: {
    isButton() {
      this.buttons.forEach((button) => {
        button.isbtn = false;
      });
    },
  },
};
</script>

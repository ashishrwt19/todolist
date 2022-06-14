<template>
  <div>
      <p>{{a}}</p>
      <button @click="sortArray">Sort</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      a: ["12:34", "02:34", "12:21", "01:12", "04:23"],
    };
  },
  methods:{
      sortArray(){
          var b=[];
          for(i = 0; i< a.length; i++){
            b[i] = a[i].slice(0,2)   
          };
          b.sort()
      }
  }
};
</script>

<style lang="scss" scoped>
</style>
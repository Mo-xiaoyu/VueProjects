<template>
  <div>
    数据统计:{{ getOrder }}
  </div>
</template>

<script>
  export default{
    name:"earth",
    data(){
      return{

      }
    },
    computed:{
      getOrder(){
        return this.$store.getters.getOrder;
      }
    }
  }
</script>

<style scoped>
</style>

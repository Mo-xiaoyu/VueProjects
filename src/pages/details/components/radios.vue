<template>
  <div class="chooser-component">
    <ul class="chooser-list">
      <li @click="choose(index)" v-for="(item,index) in RadiosContent" :class="{'active':index==nowIndex}">{{ item.title }}</li>
    </ul>
  </div>
</template>

<script>
  export default{
    name:"radios",
    data(){
      return{
        nowIndex:0
      }
    },
    props: {
      RadiosContent: {
        type: Array,
        default: function(){
          return[
            {
              title:"test",
              value:1
            }
          ]
        }
      }
    },
    methods: {
      choose(index) {
        this.nowIndex = index;
        this.$emit("radios",this.RadiosContent[index].value);
        this.$store.dispatch("updateOrder",["radios",this.RadiosContent[index].value]);
      }
    },
  }
</script>

<style scoped>
.chooser-component{
  position: relative;
  display: inline-block;
}
.chooser-list li{
  display: inline-block;
  border: 1px solid #e3e3e3;
  height: 25px;
  line-height: 25px;
  padding: 0 8px;
  margin-right: 5px;
  border-radius: 3px;
  text-align: center;
  cursor: pointer;
}
.chooser-list li.active{
  border-color: #4FC08D;
  background: #4FC08D;
  color: #fff;
}
</style>

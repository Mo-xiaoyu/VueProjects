<template>
  <div class="counter-component">
    <div class="counter-btn" @click="mins"> - </div>
    <div class="counter-show">
      <input type="text" v-model="number" @keyup="inputHandler">
    </div>
    <div class="counter-btn" @click="maxs"> + </div>

  </div>
</template>

<script>
  export default{
    name:"counter",
    data(){
      return{
        number:1
      }
    },
    props:{
      min:{
        type:Number,
        default:1
      },
      max:{
        type:Number,
        default:5
      }
    },
    methods:{
      mins(){
        if (this.number <= this.min ) {
          return;
        }
        this.number--;
        this.$emit('counter',this.number);
        this.$store.dispatch("updateOrder",["counter",this.number]);
      },
      maxs(){
        if (this.number >= this.max ) {
          return;
        }
        this.number++;
        this.$emit('counter',this.number);
        this.$store.dispatch("updateOrder",["counter",this.number]);
      },
      inputHandler(){
        // \D:非数字 /d 数字
       let fix;
       if ( typeof this.number === "string") {
         fix = Number(this.number.replace(/\D/g,''));  //g代表全局设置
       } else{
         fix = this.number;//0
       }
       if (fix > this.max || fix < this.min) {
         //把最小值给它
         fix = this.min;
       }
       this.number = fix;
       this.$emit('counter',this.number);
       this.$store.dispatch("updateOrder",["counter",this.number]);
      }
    }
  }
</script>

<style scoped>
  .counter-component{
    position: relative;
    display: inline-block;
    overflow: hidden;
    vertical-align: middle;
  }
  .counter-show{
    float: left;
  }
  .counter-show input{
    border: none;
    border-top: 1px solid #e3e3e3;
    border-bottom: 1px solid #e3e3e3;
    height: 23px;
    line-height: 23px;
    width: 30px;
    outline: none;
    text-indent: 4px;
  }
  .counter-btn{
    border: 1px solid #e3e3e3;
    float: left;
    height: 25px;
    line-height: 25px;
    width: 25px;
    text-align: center;
    cursor: pointer;
  }
 .counter-btn:hover{
   border-color: #4FC08D;
   background: #4FC08D;
   color: #fff;
 }
</style>

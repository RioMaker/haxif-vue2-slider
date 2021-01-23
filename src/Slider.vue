<template>
  <div :class="vertical==true?'slider-h':'slider-v'">
    <div class="process">
      x
    </div>
  </div>
</template>

<script>
export default {
  props:{
    vertical:{
      type:Boolean,
      default:()=>{
        return false
      }
    }
  },
  data(){
    return{

    }
  }
}
</script>

<style scoped>
.slider-h{
  width: 38px;
  height: 200px;
  box-sizing: border-box;
}
.slider-v{
  width: 200px;
  height: 38px;
  box-sizing: border-box;
}
.process{
  width: 5px;
  height: 100%;
  padding: 20px 0;
}
</style>
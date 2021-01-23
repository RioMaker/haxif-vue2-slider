<template>
<div class="xbtn">
  <div class="limiter"
    @mousemove="emitMousemove($event)"
    @mousedown="emitMousedown($event)"
    @click="emitClick($event)"
  >
    <slot>
      <div class="btn"></div>
    </slot>
  </div>
</div>
</template>

<script>
export default {
  props:{

  },
  data(){
    return{

    }
  },
  methods:{
    emitClick($event){
      this.$emit('click',$event)
    },
    emitMousemove($event){
      this.$emit('mousemove',$event)
    },
    emitMousedown($event){
      this.$emit('mousedown',$event)
    }
  }
}
</script>

<style scoped>
.limiter{
  width: fit-content;
  height: fit-content;
}
.btn{
  width: 20px;
  height: 20px;
  line-height: 20px;
  border-radius: 50%;
  text-align: center;
  transition: all .3s;
  background: #48a7ff;
}
.btn:hover{
  background: #48bbff;
}
.btn:active{
  background: #9ddffd;
}
</style>
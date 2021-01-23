<template>
  <div class="test">
    <slider 
      class="test-color"
      :vertical="true"
    >

    </slider>
  </div>
</template>

<script>
import Slider from '../src/Slider.vue';
export default {
  components:{
    Slider
  }
}
</script>

<style scoped>
.test{
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
}
.test-color{
  border: 1px solid #24ccff;
}
</style>
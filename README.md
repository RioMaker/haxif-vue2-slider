# 滑动条组件
### 安装
npm i haxif-vue2-slider --save
### 使用
```html
<!-- vue-cli组件 -->
<template>
  <!-- 
      :vertical 滑动条朝向 (true|false)(垂直|横向)
      :max 最大值 (100)
      :min 最小值 (0)
      :step 步长  (1)
      v-model 双向绑定 (默认0~100)
      :is_demo 查看测试svg
      --> 
  <div>
    <haxif-slider
      :vertical="true" 
      :max="100"
      :min="0"
      :step="1"
      v-model="a_value"
      :is_demo="true"
    >
      <!-- 你可以在这里放如svg作为自定义拖拽按钮的图标 -->
      <!-- 引用格式 -->
      <template #thumb>
        <!-- 可直接引用svg  宽高建议调整至合适即可-->
        <svg width="32" heigth="32"></svg>
      </template>
      <!-- 引用结束 -->
    </haxif-slider>
  </div>
</template>

<script>
import haxifSlider from 'haxif-vue2-slider'
export default {
  components:{
    haxifSlider
  },
  data(){
    return{
      a_value:''
    }
  }
}
</script>
```
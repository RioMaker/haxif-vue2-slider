# 滑动条组件
### 安装
npm i haxif-vue2-video --save
### 使用
```html
<!-- vue-cli组件 -->
<template>
  <!-- 
      :vertical 滑动条朝向 (true|false)(垂直|横向)
      v-on:value 获取值 (默认0~100)
      :max 最大值 (100)
      :min 最小值 (0)
      :step 步长  (1)
      --> 
  <div>
    <haxif-video
      :vertical="true" 
      v-on:value="getVal"
      :step="5"
    >
      <!-- 你可以在这里放如svg作为自定义拖拽按钮的图标 -->
    </haxif-video>
  </div>
</template>

<script>
import haxifVideo from 'haxif-vue2-video'
export default {
  components:{
    haxifVideo
  }
}
</script>
```
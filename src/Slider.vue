<template>
  <div
    :class="'slider ' + (vertical ? 'slider-v' : 'slider-h')"
    @mousemove="thumbMoveY"
    @mouseup="thumbUp"
    :style="{ '--process-color': processColor }"
  >
    <!-- 纵向拖动 -->
    <template v-if="vertical == true">
      <div
        class="process-v"
        ref="processbox"
        @click="processClick"
        :style="{
          '--clip-a': Number(25 - process / 15) + 'px',
          '--clip-b': Number((200 - process) / 2) + '%',
        }"
      ></div>
      <x-button
        class="mybtn-y"
        @click.stop=""
        @mousedown="thumbDown"
        ref="btn"
        :style="{ top: process + 'px' }"
      >
        <slot name="thumb"></slot>
      </x-button>
    </template>
    <!-- 横向拖动 -->
    <template v-else>
      <div
        class="process-h"
        ref="processbox"
        @click="processClick"
        :style="{
          '--clip-a': Number(process / 2) + '%',
          '--clip-b': Number(25 - process / 15) + 'px',
        }"
      ></div>
      <x-button
        class="mybtn-x"
        @click.stop=""
        @mousedown="thumbDown"
        ref="btn"
        :style="{ left: process + 'px' }"
      >
        <slot name="thumb"></slot>
      </x-button>
    </template>
  </div>
</template>

<script>
import xButton from "./Button.vue";
export default {
  components: {
    xButton,
  },
  props: {
    vertical: {
      type: Boolean,
      default: () => {
        return false;
      },
    },
    processColor: {
      type: String,
      default: () => {
        return "#4ec2f7";
      },
    },
    min: {
      type: Number,
      default: () => {
        return 0;
      },
    },
    max: {
      type: Number,
      default: () => {
        return 100;
      },
    },
    step:{
      type:Number,
      default:()=>{
        return 1
      }
    }
  },
  watch: {
    process(val) {
      let _cache = (((((200 - val) * (this.max - this.min)) / 200 + this.min)/this.step).toFixed(0)*this.step)
      this.$emit(
        "value",
        _cache
      );
    },
  },
  mounted() {
    // this.value_fixed =
    //   String(this.max).split(".")[1].length >
    //   String(this.min).split(".")[1].length
    //     ? String(this.max).split(".")[1].length
    //     : String(this.min).split(".")[1].length;
  },
  data() {
    return {
      // 当前拖动比
      process: 0,
      // 按住中？
      is_down: false,
      // 暂时记录移动起点
      base_x: 0,
      base_y: 0,
      //
    };
  },
  methods: {
    // 点击条上位置赋值
    processClick(e) {
      if (this.is_down) {
        return;
      } else {
        if (this.vertical) {
          this.process = e.offsetY;
        } else {
          this.process = e.offsetX;
        }
        // console.log(this.is_down);
        // console.log("cclick");
      }
    },
    // 拖拽赋值
    thumbDown(e) {
      this.is_down = true;
      this.base_y = e.clientY;
      this.base_x = e.clientX;
      // console.log("base:", this.base_y);
      window.addEventListener("mouseup", this.thumbUp, true);
      // window.addEventListener('mousemove',this.thumbMoveY,true)
    },
    thumbMoveY(e) {
      if (this.is_down) {
        let vary_y = e.clientY - this.base_y;
        let vary_x = e.clientX - this.base_x;
        let p_cache = this.process + (this.vertical ? vary_y : vary_x);
        if (p_cache <= 0) {
          this.process = 0;
        } else if (p_cache >= 200) {
          this.process = 200;
        } else {
          if (this.vertical) {
            this.process += vary_y;
            this.base_y += vary_y;
          } else {
            this.process += vary_x;
            this.base_x += vary_x;
          }
        }
        // console.log(this.process, p_cache, vary);
      }
    },
    thumbUp() {
      this.is_down = false;
      // window.removeEventListener('mouseup',this.thumbUp,true)
      // window.removeEventListener('mousemove',this.thumbMoveY,true)
    },
  },
};
</script>

<style scoped>
.slider {
  user-select: none;
  display: flex;
  justify-content: center;
  /* box-sizing: border-box; */
  position: relative;
  /* overflow: hidden; */
}
.slider-v {
  width: 30px;
  height: 220px;
}
.slider-h {
  width: 220px;
  height: 30px;
}
.process-v {
  width: 7px;
  height: 200px;
  margin-top: 10px;
  border-radius: 3px;
  position: relative;
  background: rgb(175, 175, 175);
  overflow: hidden;
}
.process-v:hover {
  cursor: pointer;
}
.process-v::after {
  content: "";
  display: block;
  width: 7px;
  height: 200px;
  border-radius: 3px;
  clip-path: ellipse(var(--clip-a) var(--clip-b) at 50% 100%);
  background: var(--process-color, #4ec2f7);
}
.process-h {
  width: 200px;
  height: 7px;
  margin-top: 10px;
  border-radius: 3px;
  position: relative;
  background: rgb(175, 175, 175);
  overflow: hidden;
}
.process-h:hover {
  cursor: pointer;
}
.process-h::after {
  content: "";
  display: block;
  width: 200px;
  height: 7px;
  border-radius: 3px;
  clip-path: ellipse(var(--clip-a) var(--clip-b) at 0% 50%);
  background: var(--process-color, #4ec2f7);
}
.mybtn-y {
  position: absolute;
  left: 50%;
  z-index: 2;
  transform: translate(-50%, calc(-50% + 10px));
  cursor: pointer;
}
.mybtn-x {
  position: absolute;
  /* left: 50%; */
  top: 50%;
  z-index: 2;
  transform: translate(calc(-50% + 10px), -50%);
  cursor: pointer;
}
</style>

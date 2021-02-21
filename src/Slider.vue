<!-- 
      :vertical 滑动条朝向
      v-on:value 获取值 0~100 
      max 最大值
      min 最小值
      step 步长
      -->
<template>
  <div class="main">
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
            '--clip-a': Number(25) + 'px',
            '--clip-b': Number(process) + '%',
          }"
        ></div>
        <x-button
          class="mybtn-y"
          @click.stop=""
          @mousedown="thumbDown"
          ref="btn"
          :style="{ top: process + 'px' }"
        >
          <slot name="thumb">
            <!-- 支持svg图标 -->
            <svg
              v-if="is_demo"
              t="1611396965803"
              class="icon"
              viewBox="0 0 1024 1024"
              version="1.1"
              xmlns="http://www.w3.org/2000/svg"
              p-id="2600"
              xmlns:xlink="http://www.w3.org/1999/xlink"
              width="32"
              height="32"
            >
              <circle cx="512" cy="512" r="420" fill="#fff"></circle>
              <path
                d="M512 937.353846c-234.732308 0-425.353846-190.621538-425.353846-425.353846 0-17.329231 14.178462-31.507692 31.507692-31.507692h236.307692c17.329231 0 31.507692 14.178462 31.507693 31.507692 0 69.316923 56.713846 126.030769 126.030769 126.030769s126.030769-56.713846 126.030769-126.030769c0-17.329231 14.178462-31.507692 31.507693-31.507692h236.307692c17.329231 0 31.507692 14.178462 31.507692 31.507692 0 234.732308-190.621538 425.353846-425.353846 425.353846zM151.236923 543.507692c15.753846 185.107692 171.716923 330.830769 360.763077 330.83077s345.009231-145.723077 360.763077-330.83077H698.683077C683.716923 632.516923 605.735385 701.046154 512 701.046154s-171.716923-68.529231-186.683077-157.538462H151.236923z"
                fill="#33363a"
                p-id="2601"
              ></path>
              <path
                d="M512 118.153846c-217.403077 0-393.846154 176.443077-393.846154 393.846154h236.307692c0-86.646154 70.892308-157.538462 157.538462-157.538462s157.538462 70.892308 157.538462 157.538462h236.307692c0-217.403077-176.443077-393.846154-393.846154-393.846154z"
                fill="#d60909"
                p-id="2602"
              ></path>
              <path
                d="M905.846154 543.507692H669.538462c-17.329231 0-31.507692-14.178462-31.507693-31.507692 0-69.316923-56.713846-126.030769-126.030769-126.030769s-126.030769 56.713846-126.030769 126.030769c0 17.329231-14.178462 31.507692-31.507693 31.507692H118.153846c-17.329231 0-31.507692-14.178462-31.507692-31.507692 0-234.732308 190.621538-425.353846 425.353846-425.353846s425.353846 190.621538 425.353846 425.353846c0 17.329231-14.178462 31.507692-31.507692 31.507692z m-207.163077-63.015384h174.867692C857.009231 295.384615 701.046154 149.661538 512 149.661538S166.990769 295.384615 151.236923 480.492308h174.867692C340.283077 391.483077 418.264615 322.953846 512 322.953846s171.716923 68.529231 186.683077 157.538462z"
                fill="#33363a"
                p-id="2603"
              ></path>
              <path
                d="M512 701.046154c-103.975385 0-189.046154-85.070769-189.046154-189.046154s85.070769-189.046154 189.046154-189.046154 189.046154 85.070769 189.046154 189.046154-85.070769 189.046154-189.046154 189.046154z m0-315.076923c-69.316923 0-126.030769 56.713846-126.030769 126.030769s56.713846 126.030769 126.030769 126.030769 126.030769-56.713846 126.030769-126.030769-56.713846-126.030769-126.030769-126.030769z"
                fill="#33363a"
                p-id="2604"
              ></path>
              <path
                d="M512 512m-78.769231 0a78.769231 78.769231 0 1 0 157.538462 0 78.769231 78.769231 0 1 0-157.538462 0Z"
                fill="#33363a"
                p-id="2605"
              ></path>
            </svg>
          </slot>
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
          <slot name="thumb">
            <!-- 支持svg图标 -->
            <svg
              v-if="is_demo"
              t="1611396965803"
              class="icon"
              viewBox="0 0 1024 1024"
              version="1.1"
              xmlns="http://www.w3.org/2000/svg"
              p-id="2600"
              xmlns:xlink="http://www.w3.org/1999/xlink"
              width="32"
              height="32"
            >
              <circle cx="512" cy="512" r="420" fill="#fff"></circle>
              <path
                d="M512 937.353846c-234.732308 0-425.353846-190.621538-425.353846-425.353846 0-17.329231 14.178462-31.507692 31.507692-31.507692h236.307692c17.329231 0 31.507692 14.178462 31.507693 31.507692 0 69.316923 56.713846 126.030769 126.030769 126.030769s126.030769-56.713846 126.030769-126.030769c0-17.329231 14.178462-31.507692 31.507693-31.507692h236.307692c17.329231 0 31.507692 14.178462 31.507692 31.507692 0 234.732308-190.621538 425.353846-425.353846 425.353846zM151.236923 543.507692c15.753846 185.107692 171.716923 330.830769 360.763077 330.83077s345.009231-145.723077 360.763077-330.83077H698.683077C683.716923 632.516923 605.735385 701.046154 512 701.046154s-171.716923-68.529231-186.683077-157.538462H151.236923z"
                fill="#33363a"
                p-id="2601"
              ></path>
              <path
                d="M512 118.153846c-217.403077 0-393.846154 176.443077-393.846154 393.846154h236.307692c0-86.646154 70.892308-157.538462 157.538462-157.538462s157.538462 70.892308 157.538462 157.538462h236.307692c0-217.403077-176.443077-393.846154-393.846154-393.846154z"
                fill="#d60909"
                p-id="2602"
              ></path>
              <path
                d="M905.846154 543.507692H669.538462c-17.329231 0-31.507692-14.178462-31.507693-31.507692 0-69.316923-56.713846-126.030769-126.030769-126.030769s-126.030769 56.713846-126.030769 126.030769c0 17.329231-14.178462 31.507692-31.507693 31.507692H118.153846c-17.329231 0-31.507692-14.178462-31.507692-31.507692 0-234.732308 190.621538-425.353846 425.353846-425.353846s425.353846 190.621538 425.353846 425.353846c0 17.329231-14.178462 31.507692-31.507692 31.507692z m-207.163077-63.015384h174.867692C857.009231 295.384615 701.046154 149.661538 512 149.661538S166.990769 295.384615 151.236923 480.492308h174.867692C340.283077 391.483077 418.264615 322.953846 512 322.953846s171.716923 68.529231 186.683077 157.538462z"
                fill="#33363a"
                p-id="2603"
              ></path>
              <path
                d="M512 701.046154c-103.975385 0-189.046154-85.070769-189.046154-189.046154s85.070769-189.046154 189.046154-189.046154 189.046154 85.070769 189.046154 189.046154-85.070769 189.046154-189.046154 189.046154z m0-315.076923c-69.316923 0-126.030769 56.713846-126.030769 126.030769s56.713846 126.030769 126.030769 126.030769 126.030769-56.713846 126.030769-126.030769-56.713846-126.030769-126.030769-126.030769z"
                fill="#33363a"
                p-id="2604"
              ></path>
              <path
                d="M512 512m-78.769231 0a78.769231 78.769231 0 1 0 157.538462 0 78.769231 78.769231 0 1 0-157.538462 0Z"
                fill="#33363a"
                p-id="2605"
              ></path>
            </svg>
          </slot>
        </x-button>
      </template>
    </div>
  </div>
</template>

<script>
import xButton from "./Button.vue";
export default {
  components: {
    xButton,
  },
  props: {
    value: {
      type: Number || String,
      default: () => {
        return 100;
      },
    },
    is_demo: {
      type: Boolean,
      default: () => {
        return false;
      },
    },
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
    step: {
      type: Number,
      default: () => {
        return 1;
      },
    },
  },
  model: {
    prop: "value",
    event: "vmodel",
  },
  watch: {
    value(val) {
      if (Number(val) != Number(this.last_emit)) {
        let result = Number(this.logic(val));
        if (result != Number(this.last_emit)) {
          // console.log(val, result);
          // let _processbox = this.vertical
          //   ? this.$refs.processbox.offsetHeight
          //   : this.$refs.processbox.offsetWidth;
          this.process_cache = val;
          // this.$emit("vmodel", String(result));
          this.last_emit = String(val);
        }
      }
    },
    process_cache(val) {
      val = Number(val)
      let result = this.logic(val);
      let _processbox = this.vertical
        ? this.$refs.processbox.offsetHeight
        : this.$refs.processbox.offsetWidth;
      // if (result != this.process) {
      // console.log('p_cache',this.max-result,this.max);
      this.last_emit = String(result);
      this.$emit("vmodel", String(result));
      this.process =
        ((this.max - result) / (this.max - this.min)) * _processbox;
      // }
    },
  },
  computed: {
    // process(){
    //   return ((this.value - this.min)/(this.max - this.min)) *200
    // }
  },
  data() {
    return {
      // 当前拖动比
      process: 0,
      process_cache: 0,
      // 按住中？
      is_down: false,
      // 暂时记录移动起点
      base_x: 0,
      base_y: 0,
      //暂存v-model值防止过度计算
      last_emit: undefined,
    };
  },
  methods: {
    // v-model
    logic(val) {
      let _cache = Number(val);
      // console.log("logic:_cache:", _cache);
      if (_cache <= this.min) {
        _cache = Number(this.min);
        // console.log(this.min);
        return this.min;
      } else if (_cache >= this.max) {
        _cache = Number(this.max);
        // console.log(this.max);
        return this.max;
      }
      // let base_step = (this.max - this.min) / this.step + 1;
      let check_list = String(
        ((_cache - this.min) / this.step).toFixed(1)
      ).split(".");
      let result =
        (Number(check_list[0]) + (Number(check_list[1]) >= 5 ? 1 : 0)) *
          this.step +
        this.min;
      // console.log("logic-checklist:", check_list);
      // console.log("logic-result:", result);
      return result;
    },
    // 点击条上位置赋值
    processClick(e) {
      if (this.is_down) {
        return;
      } else {
        let _process = this.vertical
          ? this.$refs.processbox.offsetHeight
          : this.$refs.processbox.offsetWidth;
        if (this.vertical) {
          this.process_cache =
            this.max - (e.offsetY / _process) * (this.max - this.min);
        } else {
          this.process_cache =
            this.max - (e.offsetX / _process) * (this.max - this.min);
        }
        // console.log(this.process_cache);
        // console.log(this.is_down);
        // console.log("cclick");
      }
    },
    // 拖拽赋值
    thumbDown(e) {
      this.is_down = true;
      this.base_y = e.clientY;
      this.base_x = e.clientX;
      this.process_cache = this.value;
      window.addEventListener("mouseup", this.thumbUp, true);
      // window.addEventListener('mousemove',this.thumbMoveY,true)
      // console.log("set(process_cache):", this.process_cache);
    },
    thumbMoveY(e) {
      if (this.is_down) {
        let vary_y = e.clientY - this.base_y;
        let vary_x = e.clientX - this.base_x;
        let process_max = this.vertical
          ? this.$refs.processbox.offsetHeight
          : this.$refs.processbox.offsetWidth;
        let res_y = (vary_y / Number(process_max)) * (this.max - this.min);
        let res_x = (vary_x / Number(process_max)) * (this.max - this.min);
        let p_cache = this.process_cache - (this.vertical ? res_y : res_x);
        if (p_cache < this.min) {
          this.process_cache = this.min
        } else if (p_cache > this.max) {
          this.process_cache = this.max
        } else {
          if (this.vertical) {
            this.process_cache -= res_y;
            this.base_y += vary_y;
            // console.log("cache:", this.process_cache, res_y);
          } else {
            this.process_cache -= res_x;
            this.base_x += vary_x;
          }
        }
        // console.log("cache:", this.process_cache, p_cache);
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
.main {
  width: fit-content;
  height: fit-content;
}
.slider {
  user-select: none;
  display: flex;
  width: fit-content;
  height: fit-content;
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
  clip-path: ellipse(
    var(--clip-a) calc(100% - calc(var(--clip-b) / 2)) at 50% 100%
  );
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

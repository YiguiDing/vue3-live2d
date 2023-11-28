<template>
  <!-- 使用示例 -->
  <div>
    <div style="margin: 2px 0">
      注意：如果有时候按钮不能点击，是因为模型 zIndex 挡住了按钮。
    </div>
    <div>
      <p>style：{{ style }}</p>
      <button v-text="'呆在左上角'" @click="style = LeftTop" />
      <button v-text="'呆在左下角'" @click="style = LeftBot" />
      <button v-text="'呆在右上角'" @click="style = RighTop" />
      <button v-text="'呆在右下角'" @click="style = RighBot" />
      <button v-text="'呆在中间'" @click="style = AtCentr" />
      <button v-text="'跟随流'" @click="style = Unset" />
    </div>
    <div>
      <p>isLeft：{{ isLeft }}</p>
      <button @click="isLeft = false">呆在右边</button>
      <button @click="isLeft = true">呆在左边</button>
    </div>
    <div>
      <p>resolution：</p>
      <input type="number" v-model.lazy="resolution" />
      <button @click="resolution -= 0.5">减小</button>
      <button @click="resolution += 0.5">增大</button>
    </div>
    <div>
      <p>width：</p>
      <input type="number" v-model.lazy="width" />
      <button @click="width -= 50">减小</button>
      <button @click="width += 50">增大</button>
    </div>
    <div>
      <p>height：</p>
      <input type="number" v-model.lazy="height" />
      <button @click="height -= 50">减小</button>
      <button @click="height += 50">增大</button>
    </div>
    <live2d
      class="live2d"
      v-model:width="width"
      v-model:height="height"
      v-model:resolution="resolution"
      :style="style"
      :api-path="'/vue3-live2d-static-api/indexes'"
      :model="['Potion-Maker/Pio', 'school-2017-costume-yellow']"
      :is-left="isLeft"
      :tips="tips"
    ></live2d>
  </div>
</template>

<script setup lang="ts">
/*
 * 项目中引用包时，将 import 内容替换
 * import live2d from 'vue-live2d'
 */
import live2d from "./index.vue";
import { ref, computed } from "vue";

const Unset = {};
const LeftTop = { position: "fixed", left: 0, top: 0, zIndex: 1 };
const LeftBot = { position: "fixed", left: 0, bottom: 0, zIndex: 1 };
const RighTop = { position: "fixed", right: 0, top: 0, zIndex: 1 };
const RighBot = { position: "fixed", right: 0, bottom: 0, zIndex: 1 };
const AtCentr = computed(() => {
  return {
    position: "fixed",
    left: `calc(50% - ${width.value / 2}px)`,
    top: `calc(50% - ${height.value / 2}px)`,
  };
});

let isLeft = ref(false);
let style = ref<any>(RighBot);
let width = ref(500);
let height = ref(500);
let resolution = ref(1);
let tips = ref({
  mouseover: [
    {
      selector: ".vue-live2d",
      texts: ["请查看源代码了解如何修改默认语句"],
    },
  ],
});
</script>

<style>
body {
  margin: 20px;
  padding: 0;
}
.live2d {
  border: 1px dashed gray;
}
</style>

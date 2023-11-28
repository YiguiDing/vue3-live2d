# vue3-live2d

vue 看板娘

![license](https://img.shields.io/github/license/YiguiDing/vue3-live2d)
[![version](https://img.shields.io/npm/v/vue3-live2d)](https://npm.js)
[![downloads](https://img.shields.io/npm/dt/vue3-live2d)](<https://www.npmjs.com/package/vue3-live2d> )
[![fork](https://img.shields.io/github/forks/YiguiDing/vue3-live2d?style=social)](https://github.com/YiguiDing/vue3-live2d)

该项目fork自[vue3-live2d](https://github.com/evgo2017/vue-live2d)

![logo](https://github.com/YiguiDing/vue3-live2d/blob/master/public/logo.png)

## 在线浏览

<https://vue3-live2d.vercel.app>

## 在项目中使用

```shell
npm install vue3-live2d

// 在组件中引入
import vue3Live2d from 'vue3-live2d'

// 组件中的使用方法具体参考 `src/App.vue` 文件
```

```vue
</template>
    <live2d
      class="live2d"
      v-model:width="300"
      v-model:height="300"
      v-model:resolution="2"
      :style="{ position: 'fixed', bottom: 0, right: 0, zIndex: 1 }"
      :api-path="'https://vue3-live2d.vercel.app/vue3-live2d-static-api/indexes'"
      :model="['Potion-Maker/Pio', 'school-2017-costume-yellow']"
      :tips="tips"
    />
</template>

<script setup lang="ts">
/*
 * 项目中引用包时，将 import 内容替换
 * import live2d from 'vue3-live2d'
 */
import live2d from "./index.vue";
import { ref } from "vue";
let tips = ref({
  mouseover: [
    {
      selector: ".vue3-live2d",
      texts: ["请查看源代码了解如何修改默认语句"],
    },
  ],
});
</script>
```

### 本地浏览

其中包含源码，`src/App.vue` 为使用示例。

```shell
git clone https://github.com/YiguiDing/vue3-live2d.git
cd ./vue3-live2d
npm install
# 安装子模块
git submodule update --init --recursive 
npm run dev
```

## 配置参数

### 参数说明

| 配置项      | 含义                                                                                      | 类型    | 默认                                              |
| ----------- | ----------------------------------------------------------------------------------------- | ------- | ------------------------------------------------- |
| width       | div和canvas的宽高                                                                         | Number  | 400                                               |
| height      | div和canvas的宽高                                                                         | Number  | 400                                               |
| resolution  | 决定了canvas的清晰度，`resolution=M` 则,`清晰度=width*M x height*M`，推荐值为2，          | Number  | 1                                                 |
| apiPath     | 更换模型的请求地址,推荐值 `https://vue3-live2d.vercel.app/vue3-live2d-static-api/indexes` | String  | `/vue3-live2d-static-api/indexes`                 |
| model       | 默认显示的模型，[模型号，服装号]                                                          | Array   | ['Potion-Maker/Pio', 'school-2017-costume-yello'] |
| isLeft      | 模型是否在左边                                                                            | Boolean | false                                             |
| isTipBottom | 提示框位置是否在底部                                                                      | Boolean | false                                             |
| tips        | 在触发某些事件时模型说出的话                                                              | Object  | 格式查看 /src/options/tips.js                     |
| homePage    | 可打开某页面的地址                                                                        | String  | <https://github.com/YiguiDing/vue3-live2d>        |
| customId    | 自定义 id                                                                                 | String  | vue3-live2d-main                                  |

### 具体说明

#### `apiPath` 添加获取模型的地址

1. 默认值：`/vue3-live2d-static-api/indexes`

2. 推荐值：`https://vue3-live2d.vercel.app/vue3-live2d-static-api/indexes`

3. 自定义值：
   1. 建议fork仓库： 
      1. <https://github.com/YiguiDing/vue3-live2d-static-api> 
      2. 或者 <https://github.com/evgo2017/live2d-static-api>
    2. 将模型仓库作为子仓库添加到public或是其他目录
         ```bash
         # 将模型仓库克隆到public或是其他目录
         git submodule add git@github.com:YiguiDing/vue3-live2d-static-api.git  /path/to/your/public/or/web-root/dir/live2d-static-api
         ```
    3. 修改添加模型到`??/models/` 目录下
    4. 执行脚本 `build.js`
    5. 修改 `apiPath=/你的目录/vue3-live2d-static-api/indexes`
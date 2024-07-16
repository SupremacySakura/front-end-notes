# Vue3中的一些问题及解决方案

## Vue3+elementplus+vite显示本地图片

在Vue3+vite项目中使用elementplus中的跑马灯,通过v-for渲染图片时,本地图片无法显示的问题解决:**通过import导入图片**

**错误示例:**

```vue
<script setup lang="ts">
//背景图
const backgroundImageList:string[] = [
    '@/assets/background.jpg',
    '@/assets/background.jpg2',
]

</script>
<template>
<!-- 背景图 -->
    <div class="block text-center tabBackgroundImage">
        <el-carousel height="600px">
            <el-carousel-item v-for="item in backgroundImageList" :key="item">
                <img :src="item" alt="">
            </el-carousel-item>
        </el-carousel>
    </div>
</template>
```

**正确示例:**

```vue
<script setup lang="ts">
//背景图
import backgroundImage1 from '@/assets/background.jpg'
import backgroundImage2 from '@/assets/background2.jpg'
const backgroundImageList:string[] = [
    backgroundImage1,
    backgroundImage2,
]

</script>
<template>
<!-- 背景图 -->
    <div class="block text-center tabBackgroundImage">
        <el-carousel height="600px">
            <el-carousel-item v-for="item in backgroundImageList" :key="item">
                <img :src="item" alt="">
            </el-carousel-item>
        </el-carousel>
    </div>
</template>
```

**引发错误的原因:**

使用vite工具打包时,工具会将地址识别为字符串,不会对地址进行解析.
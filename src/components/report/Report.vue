<template>
  <div>

    <!-- 面包屑导航条 -->
    <!-- 引用了Echarts文档中的折线图 npm i echarts插件-->
    <el-breadcrumb separator-class="el-icon-arrow-right">
      <el-breadcrumb-item :to="{ path: '/home' }">首页</el-breadcrumb-item>
      <el-breadcrumb-item>数据统计</el-breadcrumb-item>
      <el-breadcrumb-item>数据报表</el-breadcrumb-item>
    
    </el-breadcrumb>

    <el-card>
      <!-- 为 ECharts 准备一个具备大小（宽高）的 DOM -->
      <!-- 第一步准备一个DOM用来封装 -->
      <div id="main" style="width: 800px;height:400px;"></div>
    </el-card>
  </div>
</template>

<script>
import mix from './Report-mixins.js'
export default {
  mixins: [mix]
}
</script>
<style lang="less" scoped>
</style>

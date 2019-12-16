<template>
  <div>
    <!-- 面包屑组件 -->
    <el-breadcrumb separator-class="el-icon-arrow-right">
      <!-- to属性根据path寻找 -->
      <el-breadcrumb-item :to="{ path: '/home' }">首页</el-breadcrumb-item>
      <el-breadcrumb-item>权限管理</el-breadcrumb-item>
      <el-breadcrumb-item>权限列表</el-breadcrumb-item>
    </el-breadcrumb>
    <!-- 卡片视图 -->
    <el-card>
      <el-table
      :data="rightsList"
      border
      stripe
      style="width: 100%">
      <el-table-column type="index"></el-table-column>
      <el-table-column label="权限名称" prop="authName"></el-table-column>
      <!-- path对应访问路径 -->
      <el-table-column label="路径" prop="path"></el-table-column>
      <!-- prop="level" level接口文档中的参数名 代表权限层级 -->
      <el-table-column label="权限等级" prop="level">
        <template slot-scope="scope">
          <!-- <el-tag v-if="scope.row.level" 其中scope.row是固定写法 level接口文档的权限参数名 -->
          <el-tag v-if="scope.row.level === '0'">一级</el-tag>
          <el-tag type="success" v-else-if="scope.row.level === '1'">二级</el-tag>
          <el-tag type="warning" v-else>三级</el-tag>
        </template>
      </el-table-column>
    </el-table>
    </el-card>
  </div>
</template>
<script>
// 导入属于当前组件的 mixins
import mix from './Rights-mixins.js'
export default {
  mixins: [mix]
}
</script>

<template>
  <el-menu
    :default-active="activeIndex"
    style="
      height: 60px;
      width: 100%;
      background: rgba(255, 255, 255, 0.9);
      backdrop-filter: blur(10px);
    "
    mode="horizontal"
    :ellipsis="false"
    @select="handleSelect"
    class="fixed-menu"
  >
    <el-menu-item index="0">
      <img style="width: 80px" src="../assets/logo.png" alt="logo" />
    </el-menu-item>
    <el-menu-item index="1">首页</el-menu-item>
    <el-menu-item index="2">下载</el-menu-item>
  </el-menu>
</template>

<script lang="ts" setup>
import { ref } from 'vue'

const activeIndex = ref('1')
const handleSelect = (key: string, keyPath: string[]) => {
  console.log(key, keyPath)
}
</script>

<style scoped>
.el-menu--horizontal > .el-menu-item:nth-child(1) {
  margin-right: auto;
}

.fixed-menu {
  position: fixed;
  top: 0;
  left: 0;
  z-index: 1000;
}
</style>

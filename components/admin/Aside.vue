<template>
  <el-menu
    :default-active="$route.path"
    class="el-menu-vertical"
    router
  >
    <el-menu-item index="/admin">
      <i class="el-icon-data-line"></i>
      <span>Analytics</span>
    </el-menu-item>
    <el-menu-item index="/admin/create">
      <i class="el-icon-document-add"></i>
      <span>Create</span>
    </el-menu-item>
    <el-menu-item index="/admin/list">
      <i class="el-icon-document-copy"></i>
      <span>Posts</span>
    </el-menu-item>
    <el-menu-item index="/admin/user">
      <i class="el-icon-user"></i>
      <span>Users</span>
    </el-menu-item>
    <el-menu-item index="/admin/logout">
      <i class="el-icon-circle-close"></i>
      <span>Exit</span>
    </el-menu-item>
  </el-menu>
</template>

<script>
    export default {
        name: "Aside"
    }
</script>

<style lang="sass" scoped>
  .el-menu-vertical
    height: 100%
</style>

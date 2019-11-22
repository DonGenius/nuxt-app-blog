<template>
  <div class="admin-layout-wrap">
    <el-container class="admin-layout-container">
      <el-aside width="250px">
        <app-aside></app-aside>
      </el-aside>
      <el-main>
        <nuxt></nuxt>
      </el-main>
    </el-container>
  </div>
</template>

<script>
  import AppAside from './../components/admin/Aside'

  export default {
    components: {
      AppAside
    },
    name: "admin",
    computed: {
      error() {
        return this.$store.getters.error
      }
    },
    watch: {
      error(value) {
        this.$message.error(value.response.data.message)
      }
    }

  }
</script>

<style lang="sass" scoped>
  .admin-layout-wrap
    width: 100%
    min-height: 100vh
  .admin-layout-container
    min-height: 100vh
</style>

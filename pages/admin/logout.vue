<template>
  <div>clear data</div>
</template>

<script>
  export default {
    name: "logout",
    middleware: ['admin-auth'],
    beforeCreate() {
      this.$store.dispatch('auth/logout')
      this.$router.push('/admin/login?message=logout')
    }
  }
</script>

<style scoped>

</style>

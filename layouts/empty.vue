<template>
    <div class="empty-layout">
      <nuxt></nuxt>
    </div>
</template>

<script>
  export default {
    name: "empty",
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
  .empty-layout
    display: flex
    align-items: center
    justify-content: center
    width: 100%
    height: 100vh
</style>

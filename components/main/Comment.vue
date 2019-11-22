<template>
  <el-card class="comment">
    <header class="comment-header">
      <small>{{comment.name}}</small>
      <small>
        <i class="el-icon-time"></i>
        {{ new Date(comment.date).toLocaleString() }}
      </small>
    </header>
    <main class="comment-text">
      <p>{{comment.text}}</p>
    </main>
  </el-card>
</template>

<script>
    export default {
      name: "Comment",
      props: {
        comment: {
          type: Object,
          required: true
        }
      }
    }
</script>

<style lang="sass" scoped>
  .comment
    margin-bottom: 1rem
  .comment-header
    display: flex
    justify-content: space-between
    align-items: center
    margin-bottom: 1rem
  .comment-text
    white-space: pre-line
  footer
</style>

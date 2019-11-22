<template>
  <el-form
    :model="controls"
    :rules="rules"
    ref="form"
    @submit.native.prevent="onSubmit"
  >
    <h1>Add a comment</h1>
    <el-form-item label="Input name" prop="name">
      <el-input v-model="controls.name"></el-input>
    </el-form-item>
    <el-form-item label="Input comment" prop="text">
      <el-input
        v-model="controls.text"
        type="textarea"
        resize="none"
        :rows="2"
      ></el-input>
    </el-form-item>
    <el-form-item>
      <el-button
        type="primary"
        round
        native-type="submit"
        :loading="loading"
      >Create</el-button>
    </el-form-item>
  </el-form>
</template>

<script>
  export default {
    props: {
      postId: {
        type: String,
        required: true
      }
    },
    name: "CommentForm",
    data() {
      return {
        loading: false,
        controls: {
          name: '',
          text: ''
        },
        rules: {
          name: [
            { required: true, message: 'Please input name', trigger: 'blur' }
          ],
          text: [
            { required: true, message: 'Please input comment text', trigger: 'blur' }
          ]
        }

      }
    },
    methods: {
      onSubmit() {
        this.$refs.form.validate(async valid => {
          if (valid) {
            this.loading = true
            const formData = {
              name: this.controls.name,
              text: this.controls.text,
              postId: this.postId
            }
            try {
              const newComment = await this.$store.dispatch('comment/create', formData)
              this.$emit('created', newComment)
              this.$message.success('Comment was added')
            } catch (e) {
              this.loading = false
            }
          } else {
            console.log('error submit!!');
            return false;
          }
        })
      }
    }
  }
</script>

<style scoped>

</style>

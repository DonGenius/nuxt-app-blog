<template>
  <el-form
    :model="controls"
    :rules="rules"
    ref="form"
    @submit.native.prevent="onSubmit"
    class="create-form"
  >
    <h1 class="mb">Create new post</h1>
    <el-form-item label="Title" prop="title">
      <el-input
        v-model="controls.title"></el-input>
    </el-form-item>
    <el-form-item label="Text .md or .html" prop="text">
      <el-input
        :rows="10"
        resize="none"
        type="textarea"
        v-model="controls.text"></el-input>
    </el-form-item>

    <el-dialog
      title="Preview"
      :visible.sync="previewDialog"
    >
      <div :key="controls.text">
        <vue-markdown>{{controls.text}}</vue-markdown>
      </div>
    </el-dialog>

    <el-upload
      ref="upload"
      class="mb"
      drag
      action="https://jsonplaceholder.typicode.com/posts/"
      :on-change="handleImageChange"
      :auto-upload="false"
      >
      <i class="el-icon-upload"></i>
      <div class="el-upload__text">Drop image here or <em>click to upload</em></div>
      <div class="el-upload__tip" slot="tip">jpg/png files with a size less than 500kb</div>
    </el-upload>

    <el-form-item>
      <el-button
        type="success"
        plain
        @click.prevent="previewDialog = true"
      >Preview</el-button>
    </el-form-item>


    <el-form-item>
      <el-button
        type="primary"
        round
        native-type="submit"
        :loading="loading"
      >Create post</el-button>
    </el-form-item>
  </el-form>
</template>

<script>
  export default {
    layout: 'admin',
    middleware: ['admin-auth'],
    name: "create",
    data() {
      return {
        image: null,
        previewDialog: false,
        loading: false,
        controls: {
          title: '',
          text: '',
        },
        rules: {
          title: [
            { required: true, message: 'Please input title', trigger: 'blur' }
          ],
          text: [
            { required: true, message: 'Please input text', trigger: 'blur' }
          ],
        }

      }
    },
    methods: {
      onSubmit() {
        this.$refs.form.validate(async valid => {
          if (valid && this.image) {
            this.loading = true

            const formData = {
              title: this.controls.title,
              text: this.controls.text,
              image: this.image
            }

            try {
              await this.$store.dispatch('post/create', formData)
              this.controls.title = ''
              this.controls.text = ''
              this.$refs.upload.clearFiles()
              this.$message.success('post created')
            } catch (e) {} finally {
              this.loading = false
            }
          } else {
            this.$message.warning('form is invalid')
          }
        })
      },
      handleImageChange(file, fileList) {
        this.image = file.raw

      }
    },


  }
</script>

<style lang="sass" scoped>
  .create-form
    width: 600px
</style>

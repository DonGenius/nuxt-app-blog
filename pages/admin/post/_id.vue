<template>
  <section>
    <el-breadcrumb separator="/" class="mb">
      <el-breadcrumb-item to="admin/list">posts</el-breadcrumb-item>
      <el-breadcrumb-item>{{post.title}}</el-breadcrumb-item>
    </el-breadcrumb>

    <el-form
      :model="controls"
      :rules="rules"
      ref="form"
      @submit.native.prevent="onSubmit"
    >
<!--      <h1>Login</h1>-->
      <el-form-item label="Text .md or .html" prop="text">
        <el-input
          :rows="10"
          resize="none"
          type="textarea"
          v-model.trim="controls.text"></el-input>
      </el-form-item>
      <div class="mb">
        <small>
          <i class="el-icon-time"></i>
          <span>{{ new Date(post.date).toLocaleString() }}</span>
        </small>
        <small>
          <i class="el-icon-view"></i>
          <span>{{ post.views }}</span>
        </small>
      </div>
      <el-form-item>
        <el-button
          type="primary"
          round
          native-type="submit"
          :loading="loading"
        >Update</el-button>
      </el-form-item>
    </el-form>


  </section>

</template>

<script>
  export default {
    head() {
      return {
        title: `Post | ${this.post.title}`
      }
    },
    validate({params}) {
      return Boolean(params.id)
    },
    layout: 'admin',
    data() {
      return {
        loading: false,
        controls: {
          text: '',
        },
        rules: {
          text: [
            { required: true, message: 'Please input text', trigger: 'blur' }
          ],
        }

      }
    },
    mounted() {
      this.controls.text = this.post.text
    },
    async asyncData({store, params}) {
      const post = await store.dispatch('post/fetchAdminById', params.id)
      return {post}
    },
    methods: {
      onSubmit() {
        this.$refs.form.validate(async valid => {
          if (valid) {
            this.loading = true

            const formData = {
              text: this.controls.text,
              id: this.post._id
            }

            try {
              await this.$store.dispatch('post/update', formData)
              this.$message.success('post updated')
              this.loading = false
            } catch (e) {
              this.loading = false
            }

          }
        })
      }
    }
  }
</script>

<style lang="sass" scoped>
  section
    width: 600px
  .mb
    display: flex
    justify-content: space-between

</style>

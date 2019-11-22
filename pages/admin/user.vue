<template>
  <el-form
    :model="controls"
    :rules="rules"
    ref="form"
    @submit.native.prevent="onSubmit"
  >
    <h1>Add new user</h1>
    <el-form-item label="login" prop="login">
      <el-input v-model.trim="controls.login"></el-input>
    </el-form-item>
    <el-form-item label="password" prop="password">
      <el-input
        type="password"
        v-model.trim="controls.password"
      ></el-input>
    </el-form-item>
    <el-form-item>
      <el-button
        type="primary"
        round
        native-type="submit"
        :loading="loading"
      >add user</el-button>
    </el-form-item>
  </el-form>

</template>

<script>
  export default {
    layout: 'admin',
    middleware: ['admin-auth'],
    name: "user",
    data() {
      return {
        loading: false,
        controls: {
          login: '',
          password: ''
        },
        rules: {
          login: [
            { required: true, message: 'Please input login', trigger: 'blur' }
          ],
          password: [
            { required: true, message: 'Please input password', trigger: 'blur' },
            { min: 6, message: 'min length 6 char', trigger: 'blur' }
          ]
        }

      }
    },
    methods: {
      onSubmit() {
        this.$refs.form.validate(async valid => {
          if (valid) {
            console.log('valid')
            this.loading = true

            try {
              const formData = {
                login: this.controls.login,
                password: this.controls.password
              }
              await this.$store.dispatch('auth/createUser', formData)
              this.$message.success('User created')
              this.controls.login = ''
              this.controls.password = ''
              this.loading = false

            } catch (e) {
              console.log(e)
              this.loading = false
            }
          }
        })
      }
    }


  }
</script>

<style lang="sass" scoped>
  form
    width: 600px
</style>

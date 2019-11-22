<template>
    <el-card
      shadow="always"
      class="login-card"
    >
      <el-form
        :model="controls"
        :rules="rules"
        ref="form"
        @submit.native.prevent="onSubmit"
      >
        <h1>Login</h1>
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
          >Login</el-button>
        </el-form-item>
      </el-form>
    </el-card>
</template>

<script>
  export default {
    layout: 'empty',
    name: "login",
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
    mounted() {
      const {message} =this.$route.query
      switch (message) {
        case 'login':
          this.$message.info('login for enter to admin panel')
          break
        case 'logout':
          this.$message.success('logout complete')
          break
        case 'session':
          this.$message.warning('session is end, please login again')
          break
      }

    },
    // beforeCreate() {
    //   if (this.$store.getters['auth/isAuthenticated']) {
    //     this.$router.push('/admin?message=login')
    //   }
    // },
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
              await this.$store.dispatch('auth/login', formData)
              this.$router.push('/admin')


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
  .login-card
    width: 500px
</style>

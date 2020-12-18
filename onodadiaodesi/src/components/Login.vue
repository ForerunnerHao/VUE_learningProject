<template>
  <div class="login_bg">
    <p>this is login page 😎</p>
    <div class="login_box">
      <!-- Avatar -->
      <div class="avatar_box">
        <img src="../assets/logo.png" alt="" />
      </div>
      <!-- Form -->
      <el-form
        class="login_form"
        ref="loginFormRef"
        :model="loginForm"
        :rules="loginFormRules"
      >
        <!-- Username -->
        <el-form-item prop="username" class="login-form-item">
          <el-input
            v-model="loginForm.username"
            prefix-icon="iconfont icon-yonghu"
          ></el-input>
        </el-form-item>
        <!-- Password -->
        <el-form-item prop="password" class="login-form-item">
          <el-input
            v-model="loginForm.password"
            type="password"
            prefix-icon="iconfont icon-password1"
          ></el-input>
        </el-form-item>
        <!-- Reset -->
        <el-form-item class="login_reset">
          <el-button @click="resetLoginForm" type="text">Reset</el-button>
        </el-form-item>
        <!-- Boutton -->
        <el-form-item class="login_button">
          <el-button @click="submitLoginForm" type="primary" plain
            >Login</el-button
          >
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // 表单数据绑定对象
      loginForm: {
        username: 'admin',
        password: '123456'
      },
      loginFormRules: {
        username: [
          { required: true, message: '请输入用户名称', trigger: 'blur' },
          { min: 5, max: 20, message: '长度在 5 到 20 个字符', trigger: 'blur' }
        ],
        password: [
          { required: true, message: '请输入密码', trigger: 'blur' },
          { min: 6, max: 15, message: '长度在 6 到 15 个字符', trigger: 'blur' }
        ]
      }
    }
  },
  methods: {
    resetLoginForm() {
      this.$refs.loginFormRef.resetFields()
    },
    submitLoginForm() {
      this.$refs.loginFormRef.validate(async vaild => {
        if (!vaild) return 0
        var { data: res } = await this.$http.post('login', this.loginForm)
        console.log(res)
        if (res.meta.status !== 200) {
          return this.$message.error('登录失败,' + res.meta.msg)
        }
        this.$message.success('登录成功！')
        // token
        window.sessionStorage.setItem('token', res.data.token)
        this.$router.push('/home')
      })
    }
  }
}
</script>

<style lang="less" scoped>
.login_bg {
  background-color: #088a85;
  height: 100%;
  width: 100%;
  margin: 0px;
  padding: 0px;
  p {
    margin: 0px;
  }
}
.login_box {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  height: 350px;
  width: 400px;
  background-color: #ffffff;
  border-radius: 5px;
  box-shadow: 5px 5px 10px #0b615e;
  .avatar_box {
    width: 150px;
    height: 150px;
    padding: 10px;
    border-radius: 50%;
    border: 1px solid white;
    transform: translate(115px, -50%);
    box-shadow: 0 0 10px #0a2a29;
    background-color: #fff;
    img {
      width: 100%;
      height: 100%;
      border-radius: 50%;
      background-color: #eeeeee;
    }
  }
  .login_form {
    position: absolute;
    bottom: 30px;
    width: 100%;
    padding: 0px 50px;
    box-sizing: border-box;
    color: #086a87;
  }
  .login_button {
    display: flex;
    flex-direction: row;
    justify-content: center;
  }
  .login_button :nth-child(1) {
    width: 150px;
  }
  .login-form-item {
    margin: 20px 0px 0px 0px;
    padding: 0px;
  }
  .login_reset {
    display: flex;
    flex-direction: row;
    justify-content: flex-end;
    margin: 0px;
    padding: 0px;
  }
  .login_reset :nth-child(1) {
    margin: 0px;
    padding: 0px;
  }
}
</style>

<template>
  <div>
    <p>This is Home page 😜</p>
    <div>
      <el-button type="primary" @click="homeLogout">Log out</el-button>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    homeLogout() {
      window.sessionStorage.removeItem('token')
      const tokenStr = window.sessionStorage.getItem('token')
      if (!tokenStr) {
        this.$message('登出成功')
        this.$router.push('/login')
      }
    }
  }
}
</script>

<style lang="less" scoped></style>

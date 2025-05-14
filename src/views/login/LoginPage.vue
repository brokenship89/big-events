<script setup>
import { User, Lock } from '@element-plus/icons-vue'
import { ref } from 'vue'
const isRegister = ref(true)
</script>

<template>
  <div class="container">
    <div class="bg"></div>
    <div class="login-page">
      <div class="form">
        <h1>{{ isRegister ? '注册' : '登录' }}</h1>
        <el-input type="text" :prefix-icon="User" placeholder="请输入用户名" />
        <el-input
          type="password"
          :prefix-icon="Lock"
          placeholder="请输入密码"
        />
        <el-input
          v-if="isRegister"
          type="password"
          :prefix-icon="Lock"
          placeholder="请再次输入密码"
        />
        <div class="flex" v-else>
          <el-checkbox>记住我</el-checkbox>
          <el-link type="primary" underline="never">忘记密码？</el-link>
        </div>
        <el-button class="button" type="primary" auto-insert-space>
          {{ isRegister ? '注册' : '登录' }}
        </el-button>
        <div class="link">
          <el-link
            type="info"
            underline="never"
            @click="isRegister = !isRegister"
          >
            {{ isRegister ? '← 返回登录' : '注册 →' }}
          </el-link>
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.container {
  display: flex;
  flex-direction: row;
  height: 100vh;
  background: #fff;
}
.bg {
  flex: 1;
  background:
    url('@/assets/logo2.png') no-repeat 60% center / 240px auto,
    url('@/assets/login_bg.jpg') no-repeat center / cover;
  border-radius: 0 20px 20px 0;
}
.login-page {
  flex: 1;
  display: flex;
  justify-content: center; /* 水平居中 */
  align-items: center; /* 垂直居中 */
}
.form {
  display: flex;
  flex-direction: column;
  justify-content: center; /* 水平居中 */
  align-items: center; /* 垂直居中 */
  // padding: 20px;
  width: 60%;
  border-radius: 20px;
  gap: 30px;
  > * {
    width: 90%; /* 子元素宽度占满父容器 */
    height: 40px; /* 子元素高度统一为 50px */
  }
}
h1 {
  margin: 0; /* 去掉默认外边距 */
  font-size: 24px;
  line-height: 40px;
  display: inline-block;
}
.link {
  text-align: left;
}
.flex {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center; /* 垂直居中 */
}

@media (max-width: 768px) {
  .container {
    display: flex;
    flex-direction: column;
  }
  .bg {
    border-radius: 0px;
  }
  .form {
    width: 90%;
    max-width: 400px; /* 限制最大宽度 */
    padding: 15px;
    gap: 15px; /* 减少间距 */
  }
}
</style>

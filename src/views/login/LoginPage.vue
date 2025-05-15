<script setup>
import { User, Lock } from '@element-plus/icons-vue'
import { ref, watch } from 'vue'
import { userRegisterService } from '@/api/user.js'
import { userLoginService } from '@/api/user.js'
import { useUserStore } from '@/stores/index'
import { useRouter } from 'vue-router'
const form = ref()
const isRegister = ref(true)
const formModel = ref({
  username: '',
  password: '',
  repassword: ''
})
const rules = {
  username: [
    { required: true, message: '请输入用户名', trigger: 'blur' },
    { min: 5, max: 10, message: '用户名必须是5-10位的字符', trigger: 'blur' }
  ],
  password: [
    { required: true, message: '请输入密码', trigger: 'blur' },
    {
      pattern: /^\S{6,15}$/,
      message: '密码必须是6-15位的非空字符',
      trigger: 'blur'
    }
  ],
  repassword: [
    { required: true, message: '请再次输入密码', trigger: 'blur' },
    {
      validator: (rule, value, callback) => {
        if (value !== formModel.value.password) {
          callback(new Error('两次输入密码不一致!'))
        } else {
          callback()
        }
      },
      trigger: 'blur'
    }
  ]
}
const register = async () => {
  await form.value.validate()
  await userRegisterService(formModel.value)
  ElMessage.success('注册成功')
  isRegister.value = false
}
const router = useRouter()
const userStore = useUserStore()
const login = async () => {
  await form.value.validate()
  const res = await userLoginService(formModel.value)
  ElMessage.success('登录成功')
  userStore.setToken(res.data.token)
  router.push('/')
}
watch(isRegister, () => {
  formModel.value = {
    username: '',
    password: '',
    repassword: ''
  }
})
</script>

<template>
  <div class="container">
    <div class="bg"></div>
    <div class="login-page">
      <!-- 登录表单 -->
      <el-form
        v-if="!isRegister"
        ref="form"
        class="form"
        :model="formModel"
        :rules="rules"
      >
        <h1>登录</h1>
        <el-form-item prop="username">
          <el-input
            type="text"
            :prefix-icon="User"
            placeholder="请输入用户名"
            v-model="formModel.username"
          />
        </el-form-item>
        <el-form-item prop="password">
          <el-input
            type="password"
            :prefix-icon="Lock"
            placeholder="请输入密码"
            v-model="formModel.password"
          />
        </el-form-item>
        <el-button
          @click="login"
          class="button"
          type="primary"
          auto-insert-space
        >
          登录
        </el-button>
        <div class="link">
          <el-link
            type="info"
            underline="never"
            @click="isRegister = !isRegister"
          >
            注册 →
          </el-link>
        </div>
      </el-form>
      <!-- 注册表单 -->
      <el-form v-else class="form" ref="form" :model="formModel" :rules="rules">
        <h1>注册</h1>
        <el-form-item prop="username">
          <el-input
            type="text"
            :prefix-icon="User"
            placeholder="请输入用户名"
            v-model="formModel.username"
          />
        </el-form-item>
        <el-form-item prop="password">
          <el-input
            type="password"
            :prefix-icon="Lock"
            placeholder="请输入密码"
            v-model="formModel.password"
          />
        </el-form-item>
        <el-form-item prop="repassword">
          <el-input
            type="password"
            :prefix-icon="Lock"
            placeholder="请再次输入密码"
            v-model="formModel.repassword"
          />
        </el-form-item>
        <el-button
          @click="register"
          class="button"
          type="primary"
          auto-insert-space
        >
          注册
        </el-button>
        <div class="link">
          <el-link
            type="info"
            underline="never"
            @click="isRegister = !isRegister"
          >
            ← 登录
          </el-link>
        </div>
      </el-form>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.container {
  display: flex;
  flex-direction: row; /* 确保子元素水平排列 */
  height: 100vh;
  background-color: #fff;
  .bg {
    flex: 1;
    background:
      url('@/assets/logo2.png') no-repeat 60% center / 240px auto,
      url('@/assets/login_bg.jpg') no-repeat center / cover;
    border-radius: 0 20px 20px 0;
  }
  .login-page {
    display: flex;
    flex: 1;
    justify-content: center; /* 水平居中 */
    align-items: center; /* 垂直居中 */
  }
  ::v-deep(.el-form-item) {
    margin-bottom: 0; /* 去掉默认的下边距 */
  }
  ::v-deep(.el-input__inner) {
    height: 40px; /* 设置输入框高度 */
    line-height: 40px; /* 确保文字垂直居中 */
  }
  ::v-deep(.el-button) {
    height: 40px; /* 设置输入框高度 */
    line-height: 40px; /* 确保文字垂直居中 */
  }
  .form {
    display: flex;
    flex-direction: column;
    justify-content: center;
    user-select: none;
    width: 50vh;
    gap: 30px; /* 控制子元素之间的间距 */
  }
  h1 {
    margin: 0;
  }
  .button {
    width: 100%;
  }
  .flex {
    width: 100%;
    display: flex;
    justify-content: space-between;
    align-items: center; /* 垂直居中 */
  }
}
@media (max-width: 768px) {
  .container {
    flex-direction: column;
    .bg {
      border-radius: 0px;
    }
  }
}
</style>

<script setup>
import { useRoute, useRouter } from 'vue-router'
import { useUserStore } from '@/stores'

const route = useRoute()
const router = useRouter()
const goList = () => {
  router.push('/list')
  console.log(route, router)
}
const userStore = useUserStore()
</script>

<template>
  <div>我是app</div>
  <el-button @click="$router.push('/home')">跳首页</el-button>
  <el-button @click="goList">跳列表页</el-button>

  <p>{{ userStore.token }}</p>
  <el-button @click="userStore.setToken('abcdefg')">登录</el-button>
  <el-button @click="userStore.removeToken()">退出</el-button>
  <el-button type="primary"></el-button>
</template>

<style scoped></style>

<template>
  <div class="container">
    <div class="bg">1</div>
    <div class="login-form">2</div>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  border: 1px solid #000;
  height: 100vh;
}

/* 子元素默认左右均分 */
.container div {
  flex: 1;
}

/* 左侧背景样式 */
.bg {
  height: 100vh;
  background-color: #eee;
}

/* 右侧登录表单样式 */
.login-form {
  background: #111;
}

/* 媒体查询：当屏幕宽度小于 768px 时，改为上下布局 */
@media (max-width: 768px) {
  .container {
    flex-direction: column; /* 改为上下排列 */
  }
  .bg {
    height: 50vh; /* 调整高度 */
  }
  .login-form {
    height: 50vh; /* 调整高度 */
  }
}
</style>

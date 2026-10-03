<template>
  <div class="user-display">
    <h5>用户信息展示</h5>
    <p>姓名: {{ user.name }}</p>
    <p>角色: {{ user.role }}</p>
  </div>
</template>

<script setup>
import { inject } from 'vue'

const user = inject('user')

console.log('📄 UserDisplay: 注入了 user')
</script>

<style scoped>
.user-display {
  margin-top: 15px;
  padding: 15px;
  background: white;
  border: 1px solid #e0e0e0;
  border-radius: 6px;
}

.user-display h5 {
  color: #667eea;
  margin-bottom: 10px;
  font-size: 14px;
}
</style>

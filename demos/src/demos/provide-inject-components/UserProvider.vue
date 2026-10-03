<template>
  <div class="user-provider">
    <h4>用户信息管理（祖先组件）</h4>
    <p>当前登录用户: <strong>{{ user.name }}</strong> ({{ user.role }})</p>
    
    <!-- 深层组件 -->
    <UserDisplay />
    <UserEditor />
  </div>
</template>

<script setup>
import { ref, provide, readonly } from 'vue'
import UserDisplay from './UserDisplay.vue'
import UserEditor from './UserEditor.vue'

const user = ref({
  name: '张三',
  role: 'admin'
})

function updateUser(newName, newRole) {
  user.value = { name: newName, role: newRole }
}

// ✅ 推荐做法：提供只读数据 + 修改方法
provide('user', readonly(user))  // 数据只读
provide('updateUser', updateUser) // 提供修改方法

console.log('👤 UserProvider: 提供了 user 和 updateUser')
</script>

<style scoped>
.user-provider {
  padding: 20px;
  background: #f9f9f9;
  border: 2px solid #667eea;
  border-radius: 8px;
}

.user-provider h4 {
  color: #667eea;
  margin-bottom: 15px;
}
</style>

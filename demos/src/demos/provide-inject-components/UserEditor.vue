<template>
  <div class="user-editor">
    <h5>编辑用户信息</h5>
    <div style="display: flex; gap: 10px; margin-top: 10px;">
      <input v-model="newName" placeholder="姓名" />
      <input v-model="newRole" placeholder="角色" />
      <button class="btn" @click="handleUpdate">更新</button>
    </div>
  </div>
</template>

<script setup>
import { ref, inject } from 'vue'

const user = inject('user')
const updateUser = inject('updateUser')

const newName = ref(user.value.name)
const newRole = ref(user.value.role)

function handleUpdate() {
  updateUser(newName.value, newRole.value)
}

console.log('✏️ UserEditor: 注入了 updateUser 方法')
</script>

<style scoped>
.user-editor {
  margin-top: 15px;
  padding: 15px;
  background: white;
  border: 1px solid #e0e0e0;
  border-radius: 6px;
}

.user-editor h5 {
  color: #667eea;
  margin-bottom: 10px;
  font-size: 14px;
}

.user-editor input {
  flex: 1;
  padding: 8px;
  border: 1px solid #e0e0e0;
  border-radius: 4px;
}
</style>

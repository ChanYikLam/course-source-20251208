<template>
  <div class="user-form">
    <div class="form-group">
      <label>姓:</label>
      <input v-model="lastNameModel" />
    </div>
    
    <div class="form-group">
      <label>名:</label>
      <input v-model="firstNameModel" />
    </div>
    
    <div class="form-group">
      <label>邮箱:</label>
      <input v-model="emailModel" type="email" />
    </div>
  </div>
</template>

<script setup>
/**
 * 多个 v-model 绑定
 * 
 * 父组件使用：
 * <UserForm
 *   v-model:firstName="firstName"
 *   v-model:lastName="lastName"
 *   v-model:email="email"
 * />
 */

// 定义多个 model，使用具名参数
const firstNameModel = defineModel('firstName')
const lastNameModel = defineModel('lastName')
const emailModel = defineModel('email')

// 每个 model 都是独立的 ref，可以直接在模板中使用
</script>

<style scoped>
.user-form {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.form-group {
  display: flex;
  align-items: center;
  gap: 10px;
}

.form-group label {
  min-width: 60px;
  font-weight: 600;
  color: #667eea;
}

.form-group input {
  flex: 1;
  padding: 8px 12px;
  border: 1px solid #e0e0e0;
  border-radius: 4px;
  font-size: 14px;
}

.form-group input:focus {
  outline: none;
  border-color: #667eea;
}
</style>

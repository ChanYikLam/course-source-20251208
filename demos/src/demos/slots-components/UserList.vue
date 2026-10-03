<template>
  <ul class="user-list">
    <li v-for="(user, index) in users" :key="user.id" class="user-item">
      <!-- 作用域插槽：向父组件传递 user 和 index 数据 -->
      <slot :user="user" :index="index">
        <!-- 后备内容：如果父组件没有提供内容，显示默认样式 -->
        {{ user.name }}
      </slot>
    </li>
  </ul>
</template>

<script setup>
import { ref } from 'vue'

/**
 * 作用域插槽演示
 * 
 * 通过 :user="user" :index="index" 向插槽传递数据
 * 父组件可以通过 v-slot="{ user, index }" 接收这些数据
 */

const users = ref([
  { id: 1, name: '张三', role: 'admin' },
  { id: 2, name: '李四', role: 'user' },
  { id: 3, name: '王五', role: 'user' },
  { id: 4, name: '赵六', role: 'moderator' }
])
</script>

<style scoped>
.user-list {
  list-style: none;
  padding: 0;
  background: white;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  overflow: hidden;
}

.user-item {
  padding: 12px 20px;
  border-bottom: 1px solid #f0f0f0;
}

.user-item:last-child {
  border-bottom: none;
}

.user-item:hover {
  background: #f9f9f9;
}
</style>

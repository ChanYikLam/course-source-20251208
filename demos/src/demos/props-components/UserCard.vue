<template>
  <div class="card">
    <h3>{{ title }}</h3>
    <p>年龄: {{ age }} 岁</p>
    <p>状态: <span :style="{ color: isActive ? 'green' : 'gray' }">
      {{ isActive ? '✅ 活跃' : '⚫ 未激活' }}
    </span></p>
  </div>
</template>

<script setup>
/**
 * 演示基础类型验证
 * - title 必须是 String
 * - age 必须是 Number
 * - isActive 必须是 Boolean
 */
defineProps({
  title: String,      // 字符串类型
  age: Number,        // 数字类型
  isActive: Boolean   // 布尔类型
})
</script>

<style scoped>
.card h3 {
  color: #667eea;
  margin-bottom: 10px;
}

.card p {
  margin: 5px 0;
}
</style>

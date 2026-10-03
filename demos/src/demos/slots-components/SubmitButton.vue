<template>
  <button class="submit-btn">
    <!-- 插槽后备内容：如果父组件没有提供内容，显示"提交"文字 -->
    <slot>提交</slot>
  </button>
</template>

<script setup>
/**
 * 后备内容演示
 * 
 * <slot>提交</slot> 中的"提交"是默认内容
 * 只有当父组件没有提供内容时才会显示
 */
</script>

<style scoped>
.submit-btn {
  padding: 10px 24px;
  background: #667eea;
  color: white;
  border: none;
  border-radius: 6px;
  font-size: 14px;
  font-weight: 600;
  cursor: pointer;
  transition: background 0.3s;
}

.submit-btn:hover {
  background: #5568d3;
}

.submit-btn:active {
  transform: translateY(1px);
}
</style>

<template>
  <div class="simple-card">
    <!-- 默认插槽：父组件的内容会插入到这里 -->
    <slot></slot>
  </div>
</template>

<script setup>
/**
 * 默认插槽演示
 * <slot></slot> 会被父组件传递的内容替换
 */
</script>

<style scoped>
.simple-card {
  background: white;
  border: 2px solid #e0e0e0;
  border-radius: 8px;
  padding: 20px;
  margin: 10px 0;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}
</style>

<template>
  <div class="page-layout">
    <!-- 头部插槽 -->
    <header class="layout-header">
      <slot name="header"></slot>
    </header>
    
    <!-- 主要内容插槽（默认插槽） -->
    <main class="layout-main">
      <slot></slot>
    </main>
    
    <!-- 底部插槽 -->
    <footer class="layout-footer">
      <slot name="footer"></slot>
    </footer>
  </div>
</template>

<script setup>
/**
 * 具名插槽演示
 * - <slot name="header"></slot> 对应 <template #header>
 * - <slot></slot> 对应默认内容或 <template #default>
 * - <slot name="footer"></slot> 对应 <template #footer>
 */
</script>

<style scoped>
.page-layout {
  border: 2px solid #e0e0e0;
  border-radius: 8px;
  overflow: hidden;
  background: white;
}

.layout-header {
  padding: 20px;
  background: #f5f5f5;
  border-bottom: 1px solid #e0e0e0;
}

.layout-main {
  padding: 20px;
  min-height: 100px;
}

.layout-footer {
  padding: 15px 20px;
  background: #f5f5f5;
  border-top: 1px solid #e0e0e0;
  display: flex;
  gap: 10px;
  justify-content: flex-end;
}
</style>

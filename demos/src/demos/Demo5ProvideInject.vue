<template>
  <div>
    <h2 class="demo-title">provide / inject 深层组件通信</h2>

    <!-- 演示 1: 基础用法 -->
    <div class="example-section">
      <h3>🔗 演示 1: 跨层级传递数据</h3>
      <p>祖先组件通过 provide 提供数据，任意深度的后代组件通过 inject 获取</p>
      
      <div style="margin-top: 15px;">
        <ThemeProvider />
      </div>

      <div style="margin-top: 15px; padding: 10px; background: #e7f3ff; border-radius: 4px;">
        <strong>💡 说明：</strong>主题切换器在最顶层，但深层嵌套的按钮组件可以直接访问主题数据
      </div>
    </div>

    <!-- 演示 2: 提供响应式数据 -->
    <div class="example-section">
      <h3>⚡ 演示 2: 响应式数据 + 修改方法</h3>
      <p>provide 响应式数据和修改方法，后代组件可以读取和修改</p>
      
      <div style="margin-top: 15px;">
        <UserProvider />
      </div>
    </div>
  </div>
</template>

<script setup>
import ThemeProvider from './provide-inject-components/ThemeProvider.vue'
import UserProvider from './provide-inject-components/UserProvider.vue'
</script>

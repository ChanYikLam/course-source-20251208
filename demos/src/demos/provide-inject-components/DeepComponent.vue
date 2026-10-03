<template>
  <div class="deep-component" :class="theme">
    <h5>深层组件（使用主题）</h5>
    <p>我通过 inject 直接获取了祖先组件的主题数据</p>
    <p style="margin-top: 10px;">当前主题: <strong>{{ theme }}</strong></p>
  </div>
</template>

<script setup>
import { inject } from 'vue'

// 直接从祖先组件获取数据，无需通过 props 逐层传递
const theme = inject('theme')

console.log('🎯 DeepComponent: 注入了 theme，当前值 =', theme.value)
</script>

<style scoped>
.deep-component {
  margin-top: 15px;
  padding: 15px;
  border-radius: 6px;
  transition: all 0.3s;
}

.deep-component.light {
  background: white;
  color: #333;
  border: 2px solid #667eea;
}

.deep-component.dark {
  background: #2d2d2d;
  color: #f8f8f2;
  border: 2px solid #764ba2;
}

.deep-component h5 {
  margin-bottom: 10px;
  font-size: 14px;
}
</style>

<template>
  <div class="theme-provider">
    <h4>主题切换器（祖先组件）</h4>
    <div style="margin-bottom: 20px;">
      <button class="btn" @click="toggleTheme">
        当前主题: {{ theme }}
      </button>
    </div>
    
    <!-- 中间层组件 -->
    <MiddleComponent />
  </div>
</template>

<script setup>
import { ref, provide } from 'vue'
import MiddleComponent from './MiddleComponent.vue'

const theme = ref('light')

function toggleTheme() {
  theme.value = theme.value === 'light' ? 'dark' : 'light'
}

// 提供主题数据和切换方法
provide('theme', theme)
provide('toggleTheme', toggleTheme)

console.log('🎨 ThemeProvider: 提供了 theme 和 toggleTheme')
</script>

<style scoped>
.theme-provider {
  padding: 20px;
  background: #f9f9f9;
  border: 2px solid #667eea;
  border-radius: 8px;
}

.theme-provider h4 {
  color: #667eea;
  margin-bottom: 15px;
}
</style>

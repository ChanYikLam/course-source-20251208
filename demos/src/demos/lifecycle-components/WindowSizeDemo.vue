<template>
  <div class="window-size-demo">
    <h4>📏 当前窗口大小</h4>
    <p style="font-size: 24px; font-weight: 600; color: #667eea;">
      {{ windowWidth }} × {{ windowHeight }} px
    </p>
    <p style="color: #999; font-size: 12px;">调整浏览器窗口大小试试</p>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const windowWidth = ref(window.innerWidth)
const windowHeight = ref(window.innerHeight)

function handleResize() {
  windowWidth.value = window.innerWidth
  windowHeight.value = window.innerHeight
}

onMounted(() => {
  console.log('📏 添加 resize 事件监听')
  window.addEventListener('resize', handleResize)
})

onUnmounted(() => {
  console.log('🗑️ 移除 resize 事件监听')
  
  // ⚠️ 重要：必须移除事件监听，否则会内存泄漏！
  window.removeEventListener('resize', handleResize)
})
</script>

<style scoped>
.window-size-demo {
  padding: 20px;
  background: #f9f9f9;
  border: 2px dashed #667eea;
  border-radius: 8px;
  text-align: center;
}

.window-size-demo h4 {
  color: #667eea;
  margin-bottom: 10px;
}
</style>

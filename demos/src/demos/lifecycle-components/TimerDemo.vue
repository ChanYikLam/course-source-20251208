<template>
  <div class="timer-demo">
    <h4>⏰ 定时器演示</h4>
    <p style="font-size: 32px; font-weight: 600; color: #667eea;">{{ seconds }} 秒</p>
    <p style="color: #999; font-size: 12px;">组件卸载时会自动清理定时器</p>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const seconds = ref(0)
let timer = null  // 浏览器中 setInterval 返回 number 类型的定时器 ID

onMounted(() => {
  console.log('⏰ 启动定时器')
  
  // 每秒更新一次
  timer = setInterval(() => {
    seconds.value++
  }, 1000)
})

onUnmounted(() => {
  console.log('🛑 清理定时器')
  
  // ⚠️ 重要：必须清理定时器，否则会内存泄漏！
  if (timer) {
    clearInterval(timer)
    timer = null
  }
})
</script>

<style scoped>
.timer-demo {
  padding: 20px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border-radius: 8px;
  text-align: center;
}

.timer-demo h4 {
  margin-bottom: 10px;
}
</style>

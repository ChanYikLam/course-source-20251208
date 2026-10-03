<template>
  <div class="counter-card">
    <h3>计数器子组件</h3>
    <div class="counter-display">{{ count }}</div>
    <div style="margin-top: 15px; display: flex; gap: 10px; justify-content: center;">
      <button class="btn" @click="decrement">-</button>
      <button class="btn" @click="increment">+</button>
      <button class="btn" @click="reset">重置</button>
    </div>
    <p style="margin-top: 15px; font-size: 12px; color: #999;">
      这是一个子组件，通过 defineExpose 暴露方法
    </p>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const count = ref(0)

function increment() {
  count.value++
  console.log('➕ 子组件: increment() 被调用，count =', count.value)
}

function decrement() {
  count.value--
  console.log('➖ 子组件: decrement() 被调用，count =', count.value)
}

function reset() {
  count.value = 0
  console.log('🔄 子组件: reset() 被调用，count =', count.value)
}

// 使用 defineExpose 暴露方法和数据给父组件
// 如果不使用 defineExpose，父组件无法访问这些内容
defineExpose({
  count,       // 暴露响应式数据
  increment,   // 暴露方法
  decrement,
  reset
})
</script>

<style scoped>
.counter-card {
  padding: 20px;
  background: white;
  border: 2px solid #667eea;
  border-radius: 12px;
  text-align: center;
}

.counter-card h3 {
  margin: 0 0 15px 0;
  color: #667eea;
}

.counter-display {
  font-size: 48px;
  font-weight: bold;
  color: #667eea;
  padding: 20px;
  background: #f5f5f5;
  border-radius: 8px;
}

.btn {
  padding: 8px 16px;
  border: 2px solid #667eea;
  background: white;
  color: #667eea;
  border-radius: 6px;
  cursor: pointer;
  font-size: 14px;
  transition: all 0.3s;
}

.btn:hover {
  background: #667eea;
  color: white;
}
</style>

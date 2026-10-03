<template>
  <div class="lifecycle-demo">
    <h4>生命周期演示组件</h4>
    <p>Counter: {{ counter }}</p>
    <p style="color: #999; font-size: 12px;">打开控制台查看生命周期钩子的执行顺序</p>
  </div>
</template>

<script setup>
import { onBeforeMount, onMounted, onBeforeUpdate, onUpdated, onBeforeUnmount, onUnmounted } from 'vue'

const props = defineProps({
  counter: Number
})

// <script setup> 的顶层代码就是在 setup() 中执行的
console.log('🎬 组件初始化（setup 阶段）')

onBeforeMount(() => {
  console.log('📦 onBeforeMount: 组件即将挂载')
})

onMounted(() => {
  console.log('✅ onMounted: 组件已挂载，DOM 已可用')
})

onBeforeUpdate(() => {
  console.log('🔄 onBeforeUpdate: 数据变化，即将更新 DOM')
})

onUpdated(() => {
  console.log('✨ onUpdated: DOM 已更新完成，counter =', props.counter)
})

onBeforeUnmount(() => {
  console.log('📤 onBeforeUnmount: 组件即将卸载')
})

onUnmounted(() => {
  console.log('👋 onUnmounted: 组件已卸载')
})
</script>

<style scoped>
.lifecycle-demo {
  padding: 20px;
  background: #f9f9f9;
  border: 2px solid #667eea;
  border-radius: 8px;
}

.lifecycle-demo h4 {
  color: #667eea;
  margin-bottom: 10px;
}
</style>

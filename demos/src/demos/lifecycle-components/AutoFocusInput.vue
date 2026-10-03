<template>
  <div class="auto-focus-demo">
    <h4>🎯 自动聚焦输入框</h4>
    <input 
      ref="inputRef" 
      type="text" 
      placeholder="组件挂载时会自动聚焦到这里"
      class="focus-input"
    />
    <p style="margin-top: 10px; color: #999; font-size: 12px;">
      组件挂载后自动调用了 input.focus()
    </p>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

// 模板引用
const inputRef = ref(null)

onMounted(() => {
  console.log('🎯 自动聚焦到输入框')
  
  // DOM 已经渲染完成，可以安全地操作 DOM
  if (inputRef.value) {
    inputRef.value.focus()
  }
})
</script>

<style scoped>
.auto-focus-demo {
  padding: 20px;
  background: white;
  border: 2px solid #e0e0e0;
  border-radius: 8px;
}

.auto-focus-demo h4 {
  color: #667eea;
  margin-bottom: 15px;
}

.focus-input {
  width: 100%;
  padding: 12px;
  border: 2px solid #667eea;
  border-radius: 6px;
  font-size: 14px;
  transition: all 0.3s;
}

.focus-input:focus {
  outline: none;
  border-color: #5568d3;
  box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.2);
}
</style>

<template>
  <input
    class="custom-input"
    :value="modelValue"
    @input="$emit('update:modelValue', $event.target.value)"
    :placeholder="placeholder"
  />
</template>

<script setup>
/**
 * 传统 v-model 实现方式
 * 
 * 原理：
 * 1. 接收 modelValue 作为 prop（父组件的数据）
 * 2. 监听 input 事件，触发 update:modelValue 事件
 * 3. 父组件监听 update:modelValue 事件，更新数据
 */
defineProps({
  modelValue: String,  // 固定名称 modelValue
  placeholder: String
})

defineEmits(['update:modelValue'])  // 固定名称 update:modelValue
</script>

<style scoped>
.custom-input {
  width: 100%;
  padding: 10px;
  border: 2px solid #e0e0e0;
  border-radius: 6px;
  font-size: 14px;
  transition: border-color 0.3s;
}

.custom-input:focus {
  outline: none;
  border-color: #667eea;
}
</style>

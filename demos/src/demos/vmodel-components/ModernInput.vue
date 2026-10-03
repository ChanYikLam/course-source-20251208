<template>
  <input
    class="custom-input"
    v-model="model"
    :placeholder="placeholder"
  />
</template>

<script setup>
/**
 * Vue 3.4+ defineModel 新写法
 * 
 * 更简洁！无需手动定义 props 和 emits
 * defineModel() 返回一个 ref，可以直接读写
 */
defineProps({
  placeholder: String
})

// ✨ 新写法：一行代码搞定！
const model = defineModel()

// model 是一个 ref，可以：
// - 读取：model.value
// - 写入：model.value = '新值'
// - 在模板中双向绑定：v-model="model"
</script>

<style scoped>
.custom-input {
  width: 100%;
  padding: 10px;
  border: 2px solid #667eea;
  border-radius: 6px;
  font-size: 14px;
  box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
  transition: all 0.3s;
}

.custom-input:focus {
  outline: none;
  border-color: #5568d3;
  box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.2);
}
</style>

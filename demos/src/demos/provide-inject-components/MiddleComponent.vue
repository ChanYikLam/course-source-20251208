<template>
  <div class="middle-component">
    <h5>中间层组件（不需要主题数据）</h5>
    <p style="color: #999; font-size: 12px;">这层组件不需要主题数据，所以不用声明 props</p>
    
    <!-- 再嵌套一层 -->
    <DeepComponent />
  </div>
</template>

<script setup>
import DeepComponent from './DeepComponent.vue'

// 这个组件不需要主题数据，所以不声明任何 props
// 但它的子组件可以通过 inject 获取主题数据
</script>

<style scoped>
.middle-component {
  margin-top: 15px;
  padding: 15px;
  background: white;
  border: 2px dashed #999;
  border-radius: 6px;
}

.middle-component h5 {
  color: #999;
  margin-bottom: 10px;
  font-size: 14px;
}
</style>

<template>
  <div class="tab-content">
    <h4>🏠 首页</h4>
    <p>欢迎来到首页！</p>
    <input v-model="searchText" placeholder="搜索商品..." class="search-input" />
    <p v-if="searchText" style="margin-top: 10px;">搜索: {{ searchText }}</p>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const searchText = ref('')

onMounted(() => {
  console.log('🏠 TabHome 已挂载')
})

onUnmounted(() => {
  console.log('👋 TabHome 已销毁')
})
</script>

<script>
export default {
  name: 'TabHome' // KeepAlive 需要组件有 name
}
</script>

<style scoped>
.tab-content {
  padding: 20px;
  background: white;
  border: 1px solid #e0e0e0;
  border-radius: 0 8px 8px 8px;
  min-height: 200px;
}

.tab-content h4 {
  color: #667eea;
  margin-bottom: 15px;
}

.search-input {
  width: 100%;
  padding: 10px;
  border: 1px solid #e0e0e0;
  border-radius: 4px;
  margin-top: 10px;
}
</style>

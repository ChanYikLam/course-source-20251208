<template>
  <div class="tab-content">
    <h4>👤 个人中心</h4>
    <div style="margin-top: 15px;">
      <label>
        用户名:
        <input v-model="username" placeholder="输入用户名..." style="margin-left: 10px; padding: 5px;" />
      </label>
    </div>
    <p v-if="username" style="margin-top: 15px;">
      你好, <strong>{{ username }}</strong>！
    </p>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const username = ref('')

onMounted(() => {
  console.log('👤 TabProfile 已挂载')
})

onUnmounted(() => {
  console.log('👋 TabProfile 已销毁')
})
</script>

<script>
export default {
  name: 'TabProfile'
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
</style>

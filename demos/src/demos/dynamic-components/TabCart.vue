<template>
  <div class="tab-content">
    <h4>🛒 购物车</h4>
    <div style="margin-top: 15px;">
      <label>
        商品数量:
        <input v-model.number="itemCount" type="number" min="1" style="margin-left: 10px; padding: 5px;" />
      </label>
    </div>
    <p style="margin-top: 15px;">
      总计: <strong style="color: #667eea; font-size: 20px;">¥{{ itemCount * 99 }}</strong>
    </p>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted, onActivated, onDeactivated } from 'vue'

const itemCount = ref(1)

onMounted(() => {
  console.log('🛒 TabCart 已挂载')
})

onUnmounted(() => {
  console.log('👋 TabCart 已销毁')
})

// KeepAlive 专用钩子
onActivated(() => {
  console.log('✨ TabCart 被激活（从缓存中恢复）')
})

onDeactivated(() => {
  console.log('💤 TabCart 被停用（进入缓存）')
})
</script>

<script>
export default {
  name: 'TabCart' // ⚠️ 重要：KeepAlive include 需要匹配这个名字
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

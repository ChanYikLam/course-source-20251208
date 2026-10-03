<template>
  <span class="badge" :class="`badge-${status}`">
    {{ statusText }}
  </span>
</template>

<script setup>
import { computed } from 'vue'

/**
 * 演示自定义验证器
 * - status 只能是 'success', 'warning', 'error' 之一
 */
const props = defineProps({
  status: {
    type: String,
    // 自定义验证函数
    validator: (value) => {
      // 只允许这三个值
      const validStatuses = ['success', 'warning', 'error']
      const isValid = validStatuses.includes(value)
      
      // 如果验证失败，控制台会显示警告
      if (!isValid) {
        console.warn(`⚠️ status 必须是以下值之一: ${validStatuses.join(', ')}`)
      }
      
      return isValid
    },
    default: 'success'
  }
})

// 根据 status 显示对应的文字
const statusText = computed(() => {
  const texts = {
    success: '✅ 成功',
    warning: '⚠️ 警告',
    error: '❌ 错误'
  }
  return texts[props.status] || '未知'
})
</script>

<style scoped>
.badge {
  display: inline-block;
  padding: 6px 12px;
  border-radius: 4px;
  font-size: 14px;
  font-weight: 600;
  margin: 5px;
}

.badge-success {
  background: #d4edda;
  color: #155724;
}

.badge-warning {
  background: #fff3cd;
  color: #856404;
}

.badge-error {
  background: #f8d7da;
  color: #721c24;
}
</style>

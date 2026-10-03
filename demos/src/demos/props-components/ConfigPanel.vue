<template>
  <div class="card">
    <h3>配置面板</h3>
    <ul>
      <li>主题: {{ options.theme }}</li>
      <li>语言: {{ options.language }}</li>
      <li>通知: {{ options.notifications ? '开启' : '关闭' }}</li>
    </ul>
  </div>
</template>

<script setup>
/**
 * 演示对象/数组默认值
 * ⚠️ 对象和数组的默认值必须使用工厂函数！
 */
defineProps({
  options: {
    type: Object,
    // ✅ 正确：使用工厂函数返回对象
    default: () => ({
      theme: 'light',
      language: 'zh-CN',
      notifications: true
    })
    
    // ❌ 错误写法（不要这样写）：
    // default: { theme: 'light' }
    // 因为对象是引用类型，多个组件实例会共享同一个对象
  }
})
</script>

<style scoped>
.card h3 {
  color: #667eea;
  margin-bottom: 10px;
}

.card ul {
  list-style: none;
  padding: 0;
}

.card li {
  padding: 5px 0;
  border-bottom: 1px solid #f0f0f0;
}

.card li:last-child {
  border-bottom: none;
}
</style>

<template>
  <div class="card">
    <h3>{{ name }}</h3>
    <p>价格: ¥{{ price }}</p>
    <p>分类: {{ category }}</p>
    <p>库存状态: <span :style="{ color: inStock ? 'green' : 'red' }">
      {{ inStock ? '✅ 有货' : '❌ 缺货' }}
    </span></p>
  </div>
</template>

<script setup>
/**
 * 演示必填项和默认值
 * - name 和 price 是必填的
 * - category 和 inStock 有默认值
 */
defineProps({
  // 必填项：没有默认值
  name: {
    type: String,
    required: true  // ⚠️ 必须传递
  },
  
  price: {
    type: Number,
    required: true  // ⚠️ 必须传递
  },
  
  // 可选项：有默认值
  category: {
    type: String,
    default: '未分类'  // 默认值
  },
  
  inStock: {
    type: Boolean,
    default: true  // 默认值
  }
})
</script>

<style scoped>
.card h3 {
  color: #667eea;
  margin-bottom: 10px;
}

.card p {
  margin: 5px 0;
}
</style>

<!--
    商品列表页面
    这个页面不需要被缓存
-->
<template>
    <div class="products">
        <h2>📦 热门商品</h2>
        <p class="hint">（此页面不缓存，每次切换都会重新渲染）</p>
        
        <div class="product-list">
            <div v-for="product in products" :key="product.id" class="product-item">
                <span class="product-name">{{ product.name }}</span>
                <span class="product-price">¥{{ product.price }}</span>
                <button class="btn-add">加入购物车</button>
            </div>
        </div>
        
        <p class="render-time">渲染时间: {{ renderTime }}</p>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

// 模拟商品数据
const products = ref([
    { id: 1, name: 'Vue 3 入门教程', price: 99 },
    { id: 2, name: 'TypeScript 实战', price: 129 },
    { id: 3, name: 'Node.js 高级编程', price: 149 }
])

// 记录渲染时间，用于验证是否重新渲染
const renderTime = ref('')

onMounted(() => {
    renderTime.value = new Date().toLocaleTimeString()
    console.log('TabProducts mounted - 商品列表已渲染')
})
</script>

<style scoped>
.products h2 {
    margin-bottom: 8px;
}

.hint {
    color: #999;
    font-size: 12px;
    margin-bottom: 20px;
}

.product-list {
    display: flex;
    flex-direction: column;
    gap: 12px;
}

.product-item {
    display: flex;
    align-items: center;
    padding: 12px;
    background: #f9f9f9;
    border-radius: 8px;
}

.product-name {
    flex: 1;
    font-weight: 500;
}

.product-price {
    color: #e74c3c;
    font-weight: bold;
    margin-right: 12px;
}

.btn-add {
    padding: 6px 12px;
    background: #42b883;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}

.btn-add:hover {
    background: #3aa876;
}

.render-time {
    margin-top: 20px;
    font-size: 12px;
    color: #999;
}
</style>

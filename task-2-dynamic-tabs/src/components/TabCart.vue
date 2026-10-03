<!--
    购物车页面
    这个页面需要被 KeepAlive 缓存
    
    注意：组件需要有 name 属性才能被 KeepAlive 的 include 识别
-->
<template>
    <div class="cart">
        <h2>🛒 我的购物车</h2>
        <p class="hint">（此页面会被缓存，切换后数据保留）</p>
        
        <div class="cart-item">
            <span>Vue 3 入门教程</span>
            <div class="quantity-control">
                <button @click="quantity > 1 && quantity--">-</button>
                <input type="number" v-model.number="quantity" min="1" />
                <button @click="quantity++">+</button>
            </div>
            <span class="item-total">¥{{ 99 * quantity }}</span>
        </div>
        
        <div class="cart-total">
            <span>总计：</span>
            <span class="total-price">¥{{ 99 * quantity }}</span>
        </div>
        
        <p class="test-hint">
            💡 测试方法：修改数量，然后切换到其他 Tab，再切回来看数量是否保留
        </p>
    </div>
</template>

<script setup>
import { ref, onMounted, onActivated, onDeactivated } from 'vue'

// 商品数量 - 这个状态应该在切换 Tab 后被保留
const quantity = ref(1)

onMounted(() => {
    console.log('TabCart mounted - 购物车首次挂载')
})

// KeepAlive 特有的生命周期钩子
onActivated(() => {
    console.log('TabCart activated - 购物车被激活（从缓存恢复）')
})

onDeactivated(() => {
    console.log('TabCart deactivated - 购物车被停用（进入缓存）')
})
</script>

<!-- 
    重要：定义组件名称，用于 KeepAlive 的 include
    在 <script setup> 中需要额外的 <script> 块来定义 name
-->
<script>
export default {
    name: 'TabCart'
}
</script>

<style scoped>
.cart h2 {
    margin-bottom: 8px;
}

.hint {
    color: #42b883;
    font-size: 12px;
    margin-bottom: 20px;
}

.cart-item {
    display: flex;
    align-items: center;
    padding: 16px;
    background: #f9f9f9;
    border-radius: 8px;
    margin-bottom: 16px;
}

.cart-item > span:first-child {
    flex: 1;
    font-weight: 500;
}

.quantity-control {
    display: flex;
    align-items: center;
    gap: 8px;
    margin-right: 16px;
}

.quantity-control button {
    width: 28px;
    height: 28px;
    border: 1px solid #ddd;
    background: white;
    border-radius: 4px;
    cursor: pointer;
}

.quantity-control button:hover {
    background: #f5f5f5;
}

.quantity-control input {
    width: 50px;
    height: 28px;
    text-align: center;
    border: 1px solid #ddd;
    border-radius: 4px;
}

.item-total {
    color: #e74c3c;
    font-weight: bold;
}

.cart-total {
    display: flex;
    justify-content: flex-end;
    align-items: center;
    padding: 16px;
    border-top: 1px solid #eee;
}

.total-price {
    font-size: 24px;
    color: #e74c3c;
    font-weight: bold;
    margin-left: 8px;
}

.test-hint {
    margin-top: 20px;
    padding: 12px;
    background: #fff3cd;
    border-radius: 4px;
    font-size: 13px;
    color: #856404;
}
</style>

<!--
    个人中心页面
-->
<template>
    <div class="profile">
        <h2>👤 个人中心</h2>
        
        <div class="user-info">
            <div class="avatar">🧑‍💻</div>
            <div class="info">
                <h3>张三</h3>
                <p>zhangsan@example.com</p>
            </div>
        </div>
        
        <div class="menu-list">
            <div class="menu-item">
                <span>📦 我的订单</span>
                <span>›</span>
            </div>
            <div class="menu-item">
                <span>❤️ 我的收藏</span>
                <span>›</span>
            </div>
            <div class="menu-item">
                <span>📍 收货地址</span>
                <span>›</span>
            </div>
            <div class="menu-item">
                <span>⚙️ 设置</span>
                <span>›</span>
            </div>
        </div>
    </div>
</template>

<script setup>
import { onMounted } from 'vue'

onMounted(() => {
    console.log('TabProfile mounted - 个人中心已渲染')
})
</script>

<style scoped>
.profile h2 {
    margin-bottom: 20px;
}

.user-info {
    display: flex;
    align-items: center;
    padding: 20px;
    background: linear-gradient(135deg, #42b883, #35495e);
    border-radius: 12px;
    color: white;
    margin-bottom: 20px;
}

.avatar {
    width: 60px;
    height: 60px;
    background: white;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 30px;
    margin-right: 16px;
}

.info h3 {
    margin-bottom: 4px;
}

.info p {
    opacity: 0.8;
    font-size: 14px;
}

.menu-list {
    display: flex;
    flex-direction: column;
}

.menu-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 16px 0;
    border-bottom: 1px solid #eee;
    cursor: pointer;
}

.menu-item:hover {
    background: #f9f9f9;
    margin: 0 -20px;
    padding: 16px 20px;
}

.menu-item:last-child {
    border-bottom: none;
}
</style>

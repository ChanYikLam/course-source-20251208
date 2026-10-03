<!--
    ====================================
    Task 2：Tab 切换（动态组件）
    ====================================
    
    📌 任务目标：
    创建一个 Tab 切换组件，包含三个页面：
    1. 商品列表（TabProducts）
    2. 购物车（TabCart）- 需要缓存状态
    3. 个人中心（TabProfile）
    
    📝 要求：
    1. 使用 <component :is=""> 实现动态组件切换
    2. 使用 <KeepAlive> 缓存购物车页面的状态
    3. 购物车页面有一个数量输入框，切换 Tab 后再切回来，数值应该保留
    4. 商品列表不需要缓存（每次切换都重新渲染）
    
    💡 提示：
    - 使用 shallowRef 存储当前组件
    - KeepAlive 的 include 属性可以指定要缓存的组件
    - 组件需要有 name 属性才能被 include 识别
    
    ⏱️ 预计用时：25 分钟
-->

<template>
    <div>
        <h1>🛒 商城 Demo</h1>
        
        <!-- Tab 按钮 -->
        <div class="tabs">
            <!-- TODO: 遍历 tabs 数组，生成 Tab 按钮 -->
            <!-- 提示：点击时切换 currentTab -->
            <button
                v-for="tab in tabs"
                :key="tab.name"
                :class="['tab-btn', { active: currentTab === tab.component }]"
                @click="currentTab = tab.component"
            >
                {{ tab.icon }} {{ tab.name }}
            </button>
        </div>
        
        <!-- Tab 内容区域 -->
        <div class="tab-content">
            <!-- TODO: 使用动态组件和 KeepAlive -->
            <!-- 要求：只缓存 TabCart 组件 -->
            <!-- 提示：
            <KeepAlive include="TabCart">
                <component :is="currentTab" />
            </KeepAlive>
            -->
        </div>
    </div>
</template>

<script setup>
import { shallowRef } from 'vue'

// 导入 Tab 页面组件
import TabProducts from './components/TabProducts.vue'
import TabCart from './components/TabCart.vue'
import TabProfile from './components/TabProfile.vue'

// Tab 配置
const tabs = [
    { name: '商品列表', icon: '📦', component: TabProducts },
    { name: '购物车', icon: '🛒', component: TabCart },
    { name: '个人中心', icon: '👤', component: TabProfile }
]

// TODO: 当前激活的 Tab 组件
// 提示：使用 shallowRef 而不是 ref（性能优化）
// const currentTab = shallowRef(TabProducts)
</script>

<style scoped>
.tabs {
    display: flex;
    background: white;
    border-radius: 8px;
    overflow: hidden;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.tab-btn {
    flex: 1;
    padding: 12px 16px;
    border: none;
    background: white;
    cursor: pointer;
    font-size: 14px;
    transition: all 0.2s;
}

.tab-btn:hover {
    background: #f5f5f5;
}

.tab-btn.active {
    background: #42b883;
    color: white;
}

.tab-content {
    margin-top: 20px;
    background: white;
    border-radius: 8px;
    padding: 20px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}
</style>

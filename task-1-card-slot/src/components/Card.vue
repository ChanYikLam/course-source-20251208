<!--
    ====================================
    Card 组件
    ====================================
    
    TODO: 完成以下功能
    
    1. 创建一个带边框和阴影的卡片容器
    
    2. 定义三个插槽：
       - header：卡片标题区域（具名插槽）
       - default：卡片内容区域（默认插槽）
       - footer：卡片底部区域（具名插槽）
    
    3. header 和 footer 应该是可选的：
       - 如果父组件没有提供 header 内容，不显示 header 区域
       - 如果父组件没有提供 footer 内容，不显示 footer 区域
       - 提示：使用 $slots.xxx 或 useSlots() 判断插槽是否有内容
    
    4. 添加适当的样式
-->

<template>
    <div class="card">
        <!-- TODO: 实现 header 插槽区域 -->
        <!-- 提示：使用 v-if="$slots.header" 判断是否有内容 -->
        
        
        <!-- TODO: 实现默认插槽（内容区域） -->
        <div class="card-body">
            
        </div>
        
        
        <!-- TODO: 实现 footer 插槽区域 -->
        
    </div>
</template>

<script setup>
// 提示：可以使用 useSlots() 来获取插槽信息
// import { useSlots } from 'vue'
// const slots = useSlots()
// if (slots.header) { ... }
</script>

<style scoped>
.card {
    background: white;
    border-radius: 8px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
    overflow: hidden;
}

.card-header {
    padding: 16px;
    border-bottom: 1px solid #eee;
    background: #fafafa;
}

.card-body {
    padding: 16px;
}

.card-footer {
    padding: 16px;
    border-top: 1px solid #eee;
    background: #fafafa;
}
</style>

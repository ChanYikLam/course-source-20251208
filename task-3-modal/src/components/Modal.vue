<template>
    <!--
        TODO 5: 使用 Teleport
        
        将整个模态框包裹在 <Teleport to="body"> 中
        这样模态框会被渲染到 body 元素下，而不是当前组件内
        
        结构参考：
        <Teleport to="body">
            <div v-if="visible" class="modal-overlay" @click="close">
                模态框内容...
            </div>
        </Teleport>
    -->
    
    <!-- 在下方实现模态框结构 -->
    <div v-if="visible" class="modal-overlay">
        <!-- 
            模态框容器
            需要阻止点击事件冒泡：@click="stopPropagation"
        -->
        <div class="modal-container">
            <!-- 头部：标题 + 关闭按钮 -->
            <div class="modal-header">
                <h3>{{ title }}</h3>
                <button class="modal-close" @click="close">&times;</button>
            </div>
            
            <!-- 内容区：默认插槽 -->
            <div class="modal-body">
                <slot>默认内容</slot>
            </div>
            
            <!-- 底部：footer 具名插槽 -->
            <div class="modal-footer">
                <slot name="footer">
                    <!-- 默认的底部按钮 -->
                    <button class="btn-cancel" @click="close">关闭</button>
                </slot>
            </div>
        </div>
    </div>
    
    <!--
        完成后的结构应该是：
        
        <Teleport to="body">
            <div v-if="visible" class="modal-overlay" @click="close">
                <div class="modal-container" @click="stopPropagation">
                    <div class="modal-header">...</div>
                    <div class="modal-body"><slot /></div>
                    <div class="modal-footer"><slot name="footer" /></div>
                </div>
            </div>
        </Teleport>
    -->
</template>

<script setup>
/**
 * Modal 模态框组件
 * 
 * 功能要求：
 * 1. 使用 Teleport 将模态框渲染到 body，脱离父组件的 DOM 层级
 * 2. 实现 v-model:visible 双向绑定控制显示/隐藏
 * 3. 接收 title prop 显示标题
 * 4. 使用默认插槽放置内容
 * 5. 使用 footer 具名插槽自定义底部
 * 6. 点击遮罩层关闭模态框
 * 7. 点击模态框内部不触发关闭（阻止事件冒泡）
 */

// TODO 1: 定义 Props
// 需要定义：
// - visible: Boolean 类型，控制显示/隐藏
// - title: String 类型，模态框标题，默认值 '提示'
const props = defineProps({
    // 在这里定义 props
})

// TODO 2: 定义 Emits
// 需要定义 'update:visible' 事件用于 v-model
const emit = defineEmits([
    // 在这里定义 emit 事件
])

// TODO 3: 实现关闭方法
// 当用户点击遮罩层或关闭按钮时调用
const close = () => {
    // 提示：emit('update:visible', false)
}

// TODO 4: 阻止事件冒泡
// 防止点击模态框内部时触发遮罩层的关闭事件
const stopPropagation = (event) => {
    // 提示：event.stopPropagation()
}
</script>
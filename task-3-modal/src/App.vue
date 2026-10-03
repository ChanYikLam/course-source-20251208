<template>
    <div>
        <h1>🚀 Task 3：模态框组件</h1>
        
        <!-- 触发按钮 -->
        <button class="trigger-btn" @click="openModal">
            打开模态框
        </button>

        <!--
            TODO: 使用 Modal 组件
            
            Modal 组件需要：
            1. 接收 v-model:visible 来控制显示/隐藏
            2. 接收 title prop 来设置标题
            3. 使用默认插槽来放置内容
            4. 使用 #footer 具名插槽来自定义底部按钮
            
            示例：
            <Modal v-model:visible="showModal" title="确认操作">
                <p>这是模态框的内容...</p>
                
                <template #footer>
                    <button @click="closeModal">取消</button>
                    <button @click="handleConfirm">确认</button>
                </template>
            </Modal>
        -->

        <!-- 在下方添加 Modal 组件 -->
        <!-- TODO: 使用 Modal 组件替换下面的注释 -->
        <!-- 提示：参考上面的示例结构 -->
        
        <div class="hint">
            <p>📝 <strong>任务提示：</strong></p>
            <p>1. 完成 <code>Modal.vue</code> 组件</p>
            <p>2. 使用 <code>&lt;Teleport to="body"&gt;</code> 将模态框传送到 body</p>
            <p>3. 实现 <code>v-model:visible</code> 双向绑定</p>
            <p>4. 点击遮罩层应该关闭模态框</p>
            <p>5. 点击模态框内部不应该触发关闭</p>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue'
import Modal from './components/Modal.vue'

// TODO: 控制模态框显示/隐藏
// const showModal = ref(false)

// TODO: 打开模态框
// const openModal = () => {
//     // showModal.value = true
// }

// TODO: 关闭模态框
// const closeModal = () => {
//     // showModal.value = false
// }

// TODO: 确认操作
// const handleConfirm = () => {
//     alert('你点击了确认按钮！')
//     closeModal()
// }
</script>
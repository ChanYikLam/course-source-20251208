<template>
    <div>
        <h1>📦 Card 组件练习</h1>

        <div class="cards-container">
            <!-- 卡片1：完整的卡片（header + content + footer） -->
            <Card>
                <template #header>
                    <h3>🎉 欢迎使用</h3>
                </template>

                <p>这是卡片的主要内容区域。</p>
                <p>你可以在这里放置任何内容。</p>

                <template #footer>
                    <button class="btn btn-primary">确认</button>
                    <button class="btn">取消</button>
                </template>
            </Card>

            <!-- 卡片2：只有内容，没有 header 和 footer -->
            <Card>
                <p>这是一个简单的卡片，只有内容区域。</p>
                <p>没有标题，也没有底部按钮。</p>
            </Card>

            <!-- 卡片3：有 header，没有 footer -->
            <Card>
                <template #header>
                    <h3>📝 待办事项</h3>
                </template>

                <ul class="todo-list">
                    <li>学习 Vue 插槽</li>
                    <li>完成练习任务</li>
                    <li>复习今日内容</li>
                </ul>
            </Card>
        </div>
    </div>
</template>

<script setup>
import Card from './components/Card.vue'
</script>

<style scoped>
.cards-container {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
}

.cards-container > * {
    flex: 1;
    min-width: 280px;
}

.btn {
    padding: 8px 16px;
    border: 1px solid #ddd;
    border-radius: 4px;
    background: white;
    cursor: pointer;
    margin-right: 8px;
}

.btn:hover {
    background: #f5f5f5;
}

.btn-primary {
    background: #42b883;
    color: white;
    border-color: #42b883;
}

.btn-primary:hover {
    background: #3aa876;
}

.todo-list {
    list-style: none;
    padding: 0;
    margin: 0;
}

.todo-list li {
    padding: 8px 0;
    border-bottom: 1px dashed #eee;
}

.todo-list li:last-child {
    border-bottom: none;
}
</style>

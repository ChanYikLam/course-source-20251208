<template>
  <div>
    <h2 class="demo-title">Teleport 传送门</h2>

    <!-- 演示 1: 基础 Teleport -->
    <div class="example-section">
      <h3>🚪 演示 1: 基础模态框</h3>
      <p>点击按钮打开模态框，模态框内容会被传送到 body 末尾</p>
      
      <div style="margin-top: 15px;">
        <button class="btn" @click="showModal1 = true">打开模态框</button>
      </div>

      <!-- Teleport 到 body -->
      <Teleport to="body">
        <div v-if="showModal1" class="modal-overlay" @click="showModal1 = false">
          <div class="modal" @click.stop>
            <h3>基础模态框</h3>
            <p>这个模态框的 DOM 被传送到了 body 末尾</p>
            <button class="btn" @click="showModal1 = false">关闭</button>
          </div>
        </div>
      </Teleport>

      <div style="margin-top: 15px; padding: 10px; background: #e7f3ff; border-radius: 4px;">
        <strong>💡 说明：</strong>虽然代码写在这里，但渲染时会被移到 body 末尾<br>
        打开浏览器开发者工具可以看到模态框在 body 的最后
      </div>
    </div>

    <!-- 演示 2: 可复用的模态框组件 -->
    <div class="example-section">
      <h3>🎨 演示 2: 可复用模态框组件</h3>
      <p>封装成组件，支持插槽自定义内容</p>
      
      <div style="margin-top: 15px; display: flex; gap: 10px;">
        <button class="btn" @click="showConfirm = true">确认对话框</button>
        <button class="btn btn-secondary" @click="showForm = true">表单对话框</button>
      </div>

      <!-- 确认对话框 -->
      <Modal v-model="showConfirm">
        <template #header>
          <h3>⚠️ 确认操作</h3>
        </template>
        
        <p>你确定要执行这个操作吗？此操作不可撤销。</p>
        
        <template #footer>
          <button class="btn btn-secondary" @click="showConfirm = false">取消</button>
          <button class="btn" @click="handleConfirm">确认</button>
        </template>
      </Modal>

      <!-- 表单对话框 -->
      <Modal v-model="showForm">
        <template #header>
          <h3>📝 填写信息</h3>
        </template>
        
        <div style="display: flex; flex-direction: column; gap: 10px;">
          <input v-model="formData.name" placeholder="姓名" class="form-input" />
          <input v-model="formData.email" type="email" placeholder="邮箱" class="form-input" />
        </div>
        
        <template #footer>
          <button class="btn btn-secondary" @click="showForm = false">取消</button>
          <button class="btn" @click="handleSubmit">提交</button>
        </template>
      </Modal>
    </div>

    <!-- 演示 3: Teleport disabled -->
    <div class="example-section">
      <h3>🔧 演示 3: 禁用 Teleport</h3>
      <p>通过 :disabled="true" 可以禁用传送功能</p>
      
      <div style="margin-top: 15px;">
        <label style="display: flex; align-items: center; gap: 10px;">
          <input type="checkbox" v-model="disableTeleport" />
          禁用 Teleport（内容会在原位置渲染）
        </label>
      </div>

      <div style="margin-top: 15px;">
        <button class="btn" @click="showModal3 = true">打开模态框</button>
      </div>

      <div style="position: relative; margin-top: 15px; padding: 20px; background: #f9f9f9; border: 2px dashed #999; border-radius: 8px; min-height: 200px;">
        <p style="color: #999;">容器区域（观察模态框是否在这里渲染）</p>
        
        <Teleport to="body" :disabled="disableTeleport">
          <div v-if="showModal3" class="modal-overlay" @click="showModal3 = false">
            <div class="modal" @click.stop>
              <h3>{{ disableTeleport ? '在原位置' : '在 body' }}</h3>
              <p>当前 Teleport {{ disableTeleport ? '已禁用' : '已启用' }}</p>
              <button class="btn" @click="showModal3 = false">关闭</button>
            </div>
          </div>
        </Teleport>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import Modal from './teleport-components/Modal.vue'

const showModal1 = ref(false)
const showConfirm = ref(false)
const showForm = ref(false)
const showModal3 = ref(false)
const disableTeleport = ref(false)

const formData = ref({
  name: '',
  email: ''
})

function handleConfirm() {
  alert('操作已确认！')
  showConfirm.value = false
}

function handleSubmit() {
  alert(`提交成功！\n姓名: ${formData.value.name}\n邮箱: ${formData.value.email}`)
  showForm.value = false
}
</script>

<style scoped>
/* 模态框样式 */
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
}

.modal {
  background: white;
  padding: 30px;
  border-radius: 12px;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.3);
  max-width: 500px;
  width: 90%;
}

.modal h3 {
  margin-top: 0;
  color: #667eea;
}

.form-input {
  padding: 10px;
  border: 1px solid #e0e0e0;
  border-radius: 4px;
  font-size: 14px;
}

.form-input:focus {
  outline: none;
  border-color: #667eea;
}
</style>

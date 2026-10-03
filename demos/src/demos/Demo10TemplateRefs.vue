<template>
  <div>
    <h2 class="demo-title">模板引用 (Template Refs)</h2>

    <!-- 演示 1: 访问 DOM 元素 -->
    <div class="example-section">
      <h3>🎯 演示 1: 访问和操作 DOM 元素</h3>
      <p>使用 ref 获取 DOM 元素的引用</p>
      
      <div style="margin-top: 15px;">
        <div style="margin-bottom: 15px;">
          <input ref="inputRef" placeholder="这是一个输入框" style="padding: 10px; width: 300px;" />
        </div>

        <div style="display: flex; gap: 10px; flex-wrap: wrap;">
          <button class="btn" @click="focusInput">聚焦输入框</button>
          <button class="btn" @click="selectInput">选中文本</button>
          <button class="btn" @click="clearInput">清空输入</button>
          <button class="btn" @click="getInputInfo">获取元素信息（查看控制台）</button>
        </div>

        <div ref="scrollBox" style="
          margin-top: 15px;
          height: 200px;
          overflow-y: scroll;
          border: 2px solid #667eea;
          border-radius: 8px;
          padding: 15px;
        ">
          <p v-for="i in 20" :key="i" style="margin: 10px 0;">
            这是第 {{ i }} 行内容
          </p>
        </div>

        <div style="display: flex; gap: 10px; margin-top: 10px;">
          <button class="btn" @click="scrollToTop">滚动到顶部</button>
          <button class="btn" @click="scrollToBottom">滚动到底部</button>
        </div>
      </div>
    </div>

    <!-- 演示 2: 访问子组件实例 -->
    <div class="example-section">
      <h3>🔗 演示 2: 访问子组件实例</h3>
      <p>通过 ref 调用子组件的方法</p>
      
      <div style="margin-top: 15px;">
        <ChildCounter ref="counterRef" />

        <div style="margin-top: 15px; display: flex; gap: 10px;">
          <button class="btn" @click="incrementFromParent">父组件: 增加</button>
          <button class="btn" @click="decrementFromParent">父组件: 减少</button>
          <button class="btn" @click="resetFromParent">父组件: 重置</button>
          <button class="btn" @click="getCounterValue">获取计数值（控制台）</button>
        </div>

        <div class="info-box" style="margin-top: 15px;">
          <p><strong>💡 说明:</strong> 子组件使用 <code>defineExpose</code> 暴露方法和数据</p>
        </div>
      </div>
    </div>

    <!-- 演示 3: v-for 中的 refs -->
    <div class="example-section">
      <h3>📋 演示 3: v-for 中的模板引用</h3>
      <p>Vue 自动将元素收集到数组中（Vue 3.5+）</p>
      
      <div style="margin-top: 15px;">
        <div style="margin-bottom: 15px;">
          <input 
            v-model="newItem" 
            @keyup.enter="addItem"
            placeholder="输入内容后按回车添加" 
            style="padding: 10px; width: 300px;"
          />
          <button class="btn" @click="addItem" style="margin-left: 10px;">添加</button>
        </div>

        <div 
          v-for="(item, index) in items" 
          :key="item.id"
          ref="itemRefs"
          class="item-card"
        >
          <span>{{ item.text }}</span>
          <button class="btn-small" @click="highlightItem(index)">高亮</button>
          <button class="btn-small" @click="removeItem(index)">删除</button>
        </div>

        <div style="margin-top: 15px;">
          <button class="btn" @click="highlightAll">高亮全部</button>
          <button class="btn" @click="logItemRefs">查看所有元素引用（控制台）</button>
        </div>

        <div class="info-box" style="margin-top: 15px;">
          <p><strong>💡 说明:</strong> 直接写 <code>ref="itemRefs"</code>，Vue 会自动收集到数组</p>
        </div>
      </div>
    </div>

    <!-- 演示 4: 实际应用 - 自动聚焦 -->
    <div class="example-section">
      <h3>🌟 演示 4: 实际应用 - 表单自动聚焦</h3>
      <p>模态框打开时自动聚焦第一个输入框</p>
      
      <div style="margin-top: 15px;">
        <button class="btn" @click="showModal = true">打开登录表单</button>

        <div v-if="showModal" class="modal-overlay" @click.self="showModal = false">
          <div class="modal-content">
            <h3>用户登录</h3>
            
            <div style="margin: 20px 0;">
              <div style="margin-bottom: 15px;">
                <label>用户名:</label>
                <input 
                  ref="usernameInput"
                  type="text"
                  style="width: 100%; padding: 8px; margin-top: 5px;"
                />
              </div>

              <div style="margin-bottom: 15px;">
                <label>密码:</label>
                <input 
                  type="password"
                  style="width: 100%; padding: 8px; margin-top: 5px;"
                />
              </div>
            </div>

            <div style="display: flex; gap: 10px; justify-content: flex-end;">
              <button class="btn" @click="showModal = false">取消</button>
              <button class="btn" style="background: #667eea; color: white;">登录</button>
            </div>

            <p style="margin-top: 15px; font-size: 12px; color: #999;">
              💡 表单打开时自动聚焦到用户名输入框
            </p>
          </div>
        </div>
      </div>
    </div>

    <!-- 演示 5: 测量元素尺寸 -->
    <div class="example-section">
      <h3>📏 演示 5: 测量和监控元素尺寸</h3>
      
      <div style="margin-top: 15px;">
        <div 
          ref="resizableBox"
          :style="{
            width: boxSize.width + 'px',
            height: boxSize.height + 'px',
            background: 'linear-gradient(135deg, #667eea 0%, #764ba2 100%)',
            color: 'white',
            display: 'flex',
            alignItems: 'center',
            justifyContent: 'center',
            borderRadius: '8px',
            transition: 'all 0.3s',
            cursor: 'pointer'
          }"
          @click="randomizeSize"
        >
          <div style="text-align: center;">
            <p style="margin: 5px 0;">{{ boxSize.width }} x {{ boxSize.height }}</p>
            <p style="font-size: 12px; opacity: 0.8;">点击随机改变尺寸</p>
          </div>
        </div>

        <div class="info-box" style="margin-top: 15px;">
          <p><strong>实际渲染尺寸:</strong> {{ actualSize.width }} x {{ actualSize.height }} px</p>
          <p><strong>位置:</strong> top={{ actualSize.top }}, left={{ actualSize.left }}</p>
        </div>

        <button class="btn" style="margin-top: 10px;" @click="measureBox">
          重新测量
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, watch, nextTick } from 'vue'
import ChildCounter from './template-refs-components/ChildCounter.vue'

// 演示 1: DOM 操作
const inputRef = ref(null)
const scrollBox = ref(null)

function focusInput() {
  inputRef.value?.focus()
}

function selectInput() {
  inputRef.value?.select()
}

function clearInput() {
  if (inputRef.value) {
    inputRef.value.value = ''
    inputRef.value.focus()
  }
}

function getInputInfo() {
  if (inputRef.value) {
    console.log('📦 输入框元素信息:', {
      tagName: inputRef.value.tagName,
      value: inputRef.value.value,
      placeholder: inputRef.value.placeholder,
      width: inputRef.value.offsetWidth,
      height: inputRef.value.offsetHeight
    })
  }
}

function scrollToTop() {
  if (scrollBox.value) {
    scrollBox.value.scrollTo({ top: 0, behavior: 'smooth' })
  }
}

function scrollToBottom() {
  if (scrollBox.value) {
    scrollBox.value.scrollTo({ 
      top: scrollBox.value.scrollHeight, 
      behavior: 'smooth' 
    })
  }
}

// 演示 2: 组件引用
const counterRef = ref(null)

function incrementFromParent() {
  counterRef.value?.increment()
}

function decrementFromParent() {
  counterRef.value?.decrement()
}

function resetFromParent() {
  counterRef.value?.reset()
}

function getCounterValue() {
  if (counterRef.value) {
    console.log('🔢 当前计数值:', counterRef.value.count)
  }
}

// 演示 3: v-for refs
const items = ref([
  { id: 1, text: '列表项 1' },
  { id: 2, text: '列表项 2' },
  { id: 3, text: '列表项 3' }
])
const itemRefs = ref([])
const newItem = ref('')
let nextId = 4

function addItem() {
  if (newItem.value.trim()) {
    items.value.push({
      id: nextId++,
      text: newItem.value
    })
    newItem.value = ''
  }
}

function removeItem(index) {
  items.value.splice(index, 1)
}

function highlightItem(index) {
  const el = itemRefs.value[index]
  if (el) {
    el.style.background = '#fff3cd'
    el.style.transform = 'scale(1.05)'
    
    setTimeout(() => {
      el.style.background = ''
      el.style.transform = ''
    }, 1000)
  }
}

function highlightAll() {
  itemRefs.value.forEach((el, index) => {
    setTimeout(() => {
      highlightItem(index)
    }, index * 200)
  })
}

function logItemRefs() {
  console.log('📝 所有列表项元素引用:', itemRefs.value)
  console.log('📊 元素数量:', itemRefs.value.length)
  itemRefs.value.forEach((el, i) => {
    console.log(`  - 第 ${i} 项:`, el.textContent.trim())
  })
}

// 演示 4: 模态框自动聚焦
const showModal = ref(false)
const usernameInput = ref(null)

watch(showModal, async (isShow) => {
  if (isShow) {
    // 等待 DOM 更新后再聚焦
    await nextTick()
    usernameInput.value?.focus()
    console.log('✨ 模态框打开，自动聚焦到用户名输入框')
  }
})

// 演示 5: 测量元素
const resizableBox = ref(null)
const boxSize = ref({ width: 300, height: 200 })
const actualSize = ref({ width: 0, height: 0, top: 0, left: 0 })

function randomizeSize() {
  boxSize.value = {
    width: Math.floor(Math.random() * 300) + 200,
    height: Math.floor(Math.random() * 200) + 100
  }
  
  nextTick(() => {
    measureBox()
  })
}

function measureBox() {
  if (resizableBox.value) {
    const rect = resizableBox.value.getBoundingClientRect()
    actualSize.value = {
      width: Math.round(rect.width),
      height: Math.round(rect.height),
      top: Math.round(rect.top),
      left: Math.round(rect.left)
    }
    console.log('📏 盒子尺寸:', actualSize.value)
  }
}

onMounted(() => {
  measureBox()
})
</script>

<style scoped>
.item-card {
  padding: 15px;
  margin: 10px 0;
  background: white;
  border: 2px solid #e0e0e0;
  border-radius: 8px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  transition: all 0.3s;
}

.item-card:hover {
  border-color: #667eea;
}

.btn-small {
  padding: 5px 10px;
  margin-left: 5px;
  border: 1px solid #e0e0e0;
  background: white;
  border-radius: 4px;
  cursor: pointer;
  font-size: 12px;
}

.btn-small:hover {
  background: #f5f5f5;
}

.info-box {
  padding: 15px;
  background: #e7f3ff;
  border-radius: 8px;
  border-left: 4px solid #667eea;
}

.info-box p {
  margin: 5px 0;
}

.info-box code {
  background: rgba(102, 126, 234, 0.1);
  padding: 2px 6px;
  border-radius: 3px;
  font-family: 'Courier New', monospace;
}

.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
}

.modal-content {
  background: white;
  padding: 30px;
  border-radius: 12px;
  width: 90%;
  max-width: 400px;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.3);
}

.modal-content h3 {
  margin: 0 0 20px 0;
  color: #667eea;
}

.modal-content label {
  display: block;
  font-weight: 500;
  color: #333;
}
</style>

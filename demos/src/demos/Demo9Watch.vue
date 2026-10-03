<template>
  <div>
    <h2 class="demo-title">watch 侦听器</h2>

    <!-- 演示 1: 基础 watch -->
    <div class="example-section">
      <h3>👀 演示 1: 基础侦听（打开控制台）</h3>
      <p>侦听单个 ref</p>
      
      <div style="margin-top: 15px;">
        <input 
          v-model="searchText" 
          placeholder="输入搜索关键词..." 
          style="width: 100%; padding: 10px;"
        />
        
        <div class="log-box">
          <p><strong>搜索次数:</strong> {{ searchCount }}</p>
          <p style="color: #999; font-size: 12px;">每次输入都会触发侦听器（查看控制台）</p>
        </div>
      </div>
    </div>

    <!-- 演示 2: 深度侦听 -->
    <div class="example-section">
      <h3>🔍 演示 2: 深度侦听对象（打开控制台）</h3>
      <p>使用 deep: true 侦听嵌套属性变化</p>
      
      <div style="margin-top: 15px;">
        <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px;">
          <div>
            <h4>用户信息</h4>
            <div style="margin-bottom: 10px;">
              <label>姓名: <input v-model="user.name" style="padding: 5px;" /></label>
            </div>
            <div style="margin-bottom: 10px;">
              <label>年龄: <input v-model.number="user.age" type="number" style="padding: 5px;" /></label>
            </div>
            <div>
              <label>城市: <input v-model="user.address.city" style="padding: 5px;" /></label>
            </div>
          </div>
          
          <div class="log-box">
            <h4>变更历史</h4>
            <div v-for="(log, index) in userChangeLogs" :key="index" style="margin: 5px 0; font-size: 12px;">
              {{ log }}
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- 演示 3: immediate 选项 -->
    <div class="example-section">
      <h3>⚡ 演示 3: 立即执行（immediate）</h3>
      <p>侦听器创建时立即执行一次</p>
      
      <div style="margin-top: 15px;">
        <label>
          主题色:
          <select v-model="themeColor" style="padding: 8px; margin-left: 10px;">
            <option value="#667eea">紫色</option>
            <option value="#f093fb">粉色</option>
            <option value="#4facfe">蓝色</option>
            <option value="#43e97b">绿色</option>
          </select>
        </label>

        <div :style="{ 
          marginTop: '15px', 
          padding: '20px', 
          background: themeColor, 
          color: 'white',
          borderRadius: '8px',
          transition: 'all 0.3s'
        }">
          <p><strong>当前主题:</strong> {{ themeColor }}</p>
          <p style="font-size: 12px;">查看控制台: 组件加载时立即执行了侦听器</p>
        </div>
      </div>
    </div>

    <!-- 演示 4: 侦听多个数据源 -->
    <div class="example-section">
      <h3>🔢 演示 4: 侦听多个数据源</h3>
      <p>同时侦听多个响应式数据</p>
      
      <div style="margin-top: 15px;">
        <div style="display: flex; gap: 15px; margin-bottom: 15px;">
          <label>
            宽度: 
            <input v-model.number="rectangle.width" type="number" min="1" style="padding: 5px; width: 80px;" />
          </label>
          <label>
            高度: 
            <input v-model.number="rectangle.height" type="number" min="1" style="padding: 5px; width: 80px;" />
          </label>
        </div>

        <div 
          :style="{
            width: rectangle.width + 'px',
            height: rectangle.height + 'px',
            background: 'linear-gradient(135deg, #667eea 0%, #764ba2 100%)',
            borderRadius: '8px',
            display: 'flex',
            alignItems: 'center',
            justifyContent: 'center',
            color: 'white',
            fontSize: '14px',
            transition: 'all 0.3s'
          }"
        >
          面积: {{ rectangleArea }}
        </div>

        <div class="log-box" style="margin-top: 15px;">
          <p><strong>计算次数:</strong> {{ areaCalculations }}</p>
        </div>
      </div>
    </div>

    <!-- 演示 5: watchEffect -->
    <div class="example-section">
      <h3>🌟 演示 5: watchEffect（自动追踪依赖）</h3>
      <p>无需指定侦听目标，自动追踪回调中使用的响应式数据</p>
      
      <div style="margin-top: 15px;">
        <div style="margin-bottom: 15px;">
          <label>
            用户ID: 
            <input v-model.number="userId" type="number" min="1" max="5" style="padding: 5px;" />
          </label>
        </div>

        <div v-if="userLoading" class="loading-box">
          加载中...
        </div>

        <div v-else-if="fetchedUser" class="user-info-card">
          <h4>{{ fetchedUser.name }}</h4>
          <p>{{ fetchedUser.email }}</p>
          <p style="color: #999; font-size: 12px;">
            数据来源: JSONPlaceholder API
          </p>
        </div>
      </div>
    </div>

    <!-- 演示 6: 停止侦听器 -->
    <div class="example-section">
      <h3>🛑 演示 6: 条件停止侦听器</h3>
      <p>当满足条件时停止侦听</p>
      
      <div style="margin-top: 15px;">
        <div style="margin-bottom: 15px;">
          <label>
            计数器: 
            <input v-model.number="counter" type="number" style="padding: 5px; width: 80px;" />
          </label>
          <button class="btn" @click="counter++">+1</button>
          <button class="btn" @click="resetCounter">重置</button>
        </div>

        <div class="result-box">
          <p><strong>当前值:</strong> {{ counter }}</p>
          <p><strong>触发次数:</strong> {{ counterTriggers }}</p>
          <p :style="{ color: watcherActive ? '#43e97b' : '#999' }">
            侦听器状态: {{ watcherActive ? '✅ 运行中' : '❌ 已停止' }}
          </p>
          <p style="font-size: 12px; color: #999;">
            当计数器达到 10 时，侦听器会自动停止
          </p>
        </div>
      </div>
    </div>

    <!-- 演示 7: watch vs watchEffect 对比 -->
    <div class="example-section">
      <h3>⚖️ 演示 7: watch vs watchEffect 对比</h3>
      
      <div style="margin-top: 15px;">
        <input 
          v-model="message" 
          placeholder="输入消息..." 
          style="width: 100%; padding: 10px; margin-bottom: 15px;"
        />

        <div class="comparison">
          <div class="comparison-item">
            <h4>watch</h4>
            <ul style="font-size: 13px; color: #666;">
              <li>需要明确指定侦听目标</li>
              <li>可以访问新值和旧值</li>
              <li>默认懒执行（值变化才执行）</li>
              <li>适合: 需要对比新旧值的场景</li>
            </ul>
            <div style="margin-top: 10px; padding: 10px; background: #f0f0f0; border-radius: 4px; font-size: 12px;">
              watch 触发: {{ watchTriggers }} 次
            </div>
          </div>

          <div class="comparison-item">
            <h4>watchEffect</h4>
            <ul style="font-size: 13px; color: #666;">
              <li>自动追踪依赖（使用到的响应式数据）</li>
              <li>无法访问旧值</li>
              <li>立即执行（创建时就执行一次）</li>
              <li>适合: 副作用逻辑（如 API 请求）</li>
            </ul>
            <div style="margin-top: 10px; padding: 10px; background: #f0f0f0; border-radius: 4px; font-size: 12px;">
              watchEffect 触发: {{ watchEffectTriggers }} 次
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, watch, watchEffect } from 'vue'

// 演示 1: 基础
const searchText = ref('')
const searchCount = ref(0)

watch(searchText, (newValue, oldValue) => {
  searchCount.value++
  console.log(`🔍 搜索文本变化: "${oldValue}" → "${newValue}"`)
})

// 演示 2: 深度侦听
const user = ref({
  name: '张三',
  age: 25,
  address: {
    city: '北京'
  }
})
const userChangeLogs = ref([])

watch(user, (newValue) => {
  const timestamp = new Date().toLocaleTimeString()
  userChangeLogs.value.unshift(`[${timestamp}] 用户信息已更新`)
  console.log('👤 用户对象变化:', newValue)
  
  // 限制日志条数
  if (userChangeLogs.value.length > 5) {
    userChangeLogs.value.pop()
  }
}, { deep: true })

// 演示 3: immediate
const themeColor = ref('#667eea')

watch(themeColor, (newColor) => {
  console.log('🎨 主题色变化:', newColor)
  // 这里可以执行副作用，如保存到 localStorage
  localStorage.setItem('theme', newColor)
}, { immediate: true })  // 组件加载时立即执行

// 演示 4: 多数据源
const rectangle = ref({
  width: 200,
  height: 100
})
const rectangleArea = ref(0)
const areaCalculations = ref(0)

watch([() => rectangle.value.width, () => rectangle.value.height], ([newWidth, newHeight]) => {
  rectangleArea.value = newWidth * newHeight
  areaCalculations.value++
  console.log(`📐 矩形尺寸变化: ${newWidth} x ${newHeight} = ${rectangleArea.value}`)
})

// 演示 5: watchEffect
const userId = ref(1)
const fetchedUser = ref(null)
const userLoading = ref(false)

watchEffect(async () => {
  userLoading.value = true
  console.log('🌐 watchEffect 自动触发，获取用户数据:', userId.value)
  
  try {
    const response = await fetch(`https://jsonplaceholder.typicode.com/users/${userId.value}`)
    fetchedUser.value = await response.json()
  } catch (error) {
    console.error('获取用户失败:', error)
  } finally {
    userLoading.value = false
  }
})

// 演示 6: 停止侦听
const counter = ref(0)
const counterTriggers = ref(0)
const watcherActive = ref(true)

const stopWatcher = watch(counter, (newValue) => {
  counterTriggers.value++
  console.log('⏱️ 计数器变化:', newValue)
  
  if (newValue >= 10) {
    console.log('🛑 计数器达到 10，停止侦听器')
    stopWatcher()  // 调用返回的函数停止侦听
    watcherActive.value = false
  }
})

function resetCounter() {
  counter.value = 0
  counterTriggers.value = 0
  watcherActive.value = true
  
  // 重新启动侦听器
  const newStopWatcher = watch(counter, (newValue) => {
    counterTriggers.value++
    console.log('⏱️ 计数器变化:', newValue)
    
    if (newValue >= 10) {
      console.log('🛑 计数器达到 10，停止侦听器')
      newStopWatcher()
      watcherActive.value = false
    }
  })
}

// 演示 7: 对比
const message = ref('')
const watchTriggers = ref(0)
const watchEffectTriggers = ref(0)

watch(message, (newVal, oldVal) => {
  watchTriggers.value++
  console.log(`watch: "${oldVal}" → "${newVal}"`)
})

watchEffect(() => {
  watchEffectTriggers.value++
  console.log('watchEffect: message =', message.value)
})
</script>

<style scoped>
.log-box {
  padding: 15px;
  background: #f9f9f9;
  border-left: 4px solid #667eea;
  border-radius: 4px;
  margin-top: 15px;
}

.result-box {
  padding: 15px;
  background: #f9f9f9;
  border-left: 4px solid #667eea;
  border-radius: 4px;
}

.loading-box {
  padding: 20px;
  text-align: center;
  color: #999;
  background: #f5f5f5;
  border-radius: 8px;
}

.user-info-card {
  padding: 20px;
  background: white;
  border: 2px solid #667eea;
  border-radius: 8px;
}

.user-info-card h4 {
  margin: 0 0 10px 0;
  color: #667eea;
}

.user-info-card p {
  margin: 5px 0;
}

.comparison {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 20px;
}

.comparison-item {
  padding: 15px;
  border: 2px solid #e0e0e0;
  border-radius: 8px;
}

.comparison-item h4 {
  color: #667eea;
  margin-bottom: 10px;
  font-size: 14px;
}

.comparison-item ul {
  margin: 0;
  padding-left: 20px;
}

.comparison-item li {
  margin: 8px 0;
  line-height: 1.6;
}
</style>

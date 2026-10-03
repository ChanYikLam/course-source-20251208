<template>
  <div>
    <h2 class="demo-title">computed 计算属性</h2>

    <!-- 演示 1: 基础computed -->
    <div class="example-section">
      <h3>🧮 演示 1: 基础计算属性</h3>
      <p>自动追踪依赖并缓存结果</p>
      
      <div style="margin-top: 15px;">
        <div style="display: flex; gap: 10px; margin-bottom: 15px;">
          <div>
            <label>姓: <input v-model="firstName" style="padding: 5px;" /></label>
          </div>
          <div>
            <label>名: <input v-model="lastName" style="padding: 5px;" /></label>
          </div>
        </div>
        
        <div class="result-box">
          <p><strong>全名:</strong> {{ fullName }}</p>
        </div>
      </div>

      <div style="margin-top: 15px; padding: 10px; background: #e7f3ff; border-radius: 4px;">
        <strong>💡 说明:</strong> fullName 会自动追踪 firstName 和 lastName 的变化
      </div>
    </div>

    <!-- 演示 2: computed vs 方法 -->
    <div class="example-section">
      <h3>⚡ 演示 2: 计算属性 vs 方法（打开控制台）</h3>
      <p>计算属性有缓存，方法每次都执行</p>
      
      <div style="margin-top: 15px;">
        <div style="margin-bottom: 15px;">
          <label>
            数字: <input v-model.number="number" type="number" style="padding: 5px;" />
          </label>
          <button class="btn" @click="renderCount++">强制重新渲染 ({{ renderCount }})</button>
        </div>

        <div class="comparison">
          <div class="comparison-item">
            <h4>使用方法 (每次渲染都计算)</h4>
            <p>{{ doubleByMethod() }}</p>
            <p>{{ doubleByMethod() }}</p>
            <p>{{ doubleByMethod() }}</p>
            <small style="color: #999;">查看控制台：每次都输出 3 次</small>
          </div>

          <div class="comparison-item">
            <h4>使用计算属性 (缓存结果)</h4>
            <p>{{ doubleByComputed }}</p>
            <p>{{ doubleByComputed }}</p>
            <p>{{ doubleByComputed }}</p>
            <small style="color: #999;">查看控制台：只计算 1 次</small>
          </div>
        </div>
      </div>
    </div>

    <!-- 演示 3: 可写计算属性 -->
    <div class="example-section">
      <h3>✍️ 演示 3: 可写计算属性</h3>
      <p>定义 getter 和 setter</p>
      
      <div style="margin-top: 15px;">
        <div style="margin-bottom: 15px;">
          <label>直接编辑全名: <input v-model="editableFullName" style="padding: 5px; width: 200px;" /></label>
        </div>

        <div class="result-box">
          <p><strong>姓:</strong> {{ firstName }}</p>
          <p><strong>名:</strong> {{ lastName }}</p>
          <p style="color: #999; font-size: 12px;">输入格式如: "张三" (姓在前，名在后)</p>
        </div>
      </div>
    </div>

    <!-- 演示 4: 实际应用 - 购物车 -->
    <div class="example-section">
      <h3>🛒 演示 4: 实际应用 - 购物车总价</h3>
      
      <div style="margin-top: 15px;">
        <table>
          <thead>
            <tr>
              <th>商品</th>
              <th>单价</th>
              <th>数量</th>
              <th>小计</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="item in cart" :key="item.id">
              <td>{{ item.name }}</td>
              <td>¥{{ item.price }}</td>
              <td>
                <button @click="item.count--" :disabled="item.count <= 1">-</button>
                {{ item.count }}
                <button @click="item.count++">+</button>
              </td>
              <td>¥{{ (item.price * item.count).toLocaleString() }}</td>
            </tr>
          </tbody>
        </table>

        <div class="total-box">
          <p>商品总数: <strong>{{ totalItems }}</strong> 件</p>
          <p>总价: <strong style="color: #667eea; font-size: 24px;">{{ formattedTotal }}</strong></p>
        </div>
      </div>
    </div>

    <!-- 演示 5: 过滤列表 -->
    <div class="example-section">
      <h3>🔍 演示 5: 搜索过滤</h3>
      
      <div style="margin-top: 15px;">
        <input 
          v-model="searchQuery" 
          placeholder="搜索用户名..." 
          style="width: 100%; padding: 10px; margin-bottom: 15px;"
        />

        <div style="display: grid; grid-template-columns: repeat(auto-fill, minmax(200px, 1fr)); gap: 10px;">
          <div v-for="user in filteredUsers" :key="user.id" class="user-card">
            <h4>{{ user.name }}</h4>
            <p style="color: #999; font-size: 12px;">{{ user.email }}</p>
          </div>
        </div>

        <p style="margin-top: 15px; color: #999;">
          找到 {{ filteredUsers.length }} / {{ users.length }} 个用户
        </p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

// 演示 1: 基础
const firstName = ref('张')
const lastName = ref('三')

const fullName = computed(() => {
  return firstName.value + lastName.value
})

// 演示 2: 对比
const number = ref(5)
const renderCount = ref(0)

function doubleByMethod() {
  console.log('⚠️ 方法被调用')
  return number.value * 2
}

const doubleByComputed = computed(() => {
  console.log('✅ 计算属性被计算')
  return number.value * 2
})

// 演示 3: 可写
const editableFullName = computed({
  get() {
    return firstName.value + lastName.value
  },
  set(newValue) {
    if (newValue.length >= 2) {
      firstName.value = newValue[0]
      lastName.value = newValue.slice(1)
    }
  }
})

// 演示 4: 购物车
const cart = ref([
  { id: 1, name: 'iPhone 15 Pro', price: 7999, count: 1 },
  { id: 2, name: 'iPad Air', price: 3999, count: 2 },
  { id: 3, name: 'MacBook Pro', price: 12999, count: 1 }
])

const totalItems = computed(() => {
  return cart.value.reduce((sum, item) => sum + item.count, 0)
})

const totalPrice = computed(() => {
  return cart.value.reduce((sum, item) => sum + item.price * item.count, 0)
})

const formattedTotal = computed(() => {
  return '¥' + totalPrice.value.toLocaleString()
})

// 演示 5: 过滤
const searchQuery = ref('')
const users = ref([
  { id: 1, name: '张三', email: 'zhangsan@example.com' },
  { id: 2, name: '李四', email: 'lisi@example.com' },
  { id: 3, name: '王五', email: 'wangwu@example.com' },
  { id: 4, name: '赵六', email: 'zhaoliu@example.com' },
  { id: 5, name: '钱七', email: 'qianqi@example.com' }
])

const filteredUsers = computed(() => {
  const query = searchQuery.value.toLowerCase()
  if (!query) return users.value
  
  return users.value.filter(user => {
    return user.name.toLowerCase().includes(query) ||
           user.email.toLowerCase().includes(query)
  })
})
</script>

<style scoped>
.result-box {
  padding: 15px;
  background: #f9f9f9;
  border-left: 4px solid #667eea;
  border-radius: 4px;
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

.total-box {
  margin-top: 20px;
  padding: 20px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border-radius: 8px;
  text-align: right;
}

.total-box p {
  margin: 5px 0;
}

.user-card {
  padding: 15px;
  background: white;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  transition: all 0.3s;
}

.user-card:hover {
  border-color: #667eea;
  box-shadow: 0 2px 8px rgba(102, 126, 234, 0.2);
}

.user-card h4 {
  margin: 0 0 5px 0;
  color: #667eea;
}

table button {
  padding: 2px 8px;
  margin: 0 5px;
  border: 1px solid #e0e0e0;
  background: white;
  border-radius: 3px;
  cursor: pointer;
}

table button:hover:not(:disabled) {
  background: #f5f5f5;
}

table button:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}
</style>

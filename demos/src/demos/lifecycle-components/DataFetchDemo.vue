<template>
  <div class="data-fetch-demo">
    <h4>📊 用户数据</h4>
    
    <!-- 加载状态 -->
    <div v-if="loading" style="text-align: center; padding: 20px;">
      <div class="spinner"></div>
      <p style="color: #999; margin-top: 10px;">加载中...</p>
    </div>
    
    <!-- 错误状态 -->
    <div v-else-if="error" style="padding: 20px; background: #f8d7da; color: #721c24; border-radius: 4px;">
      ❌ 加载失败: {{ error }}
    </div>
    
    <!-- 数据展示 -->
    <div v-else>
      <table>
        <thead>
          <tr>
            <th>ID</th>
            <th>姓名</th>
            <th>邮箱</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="user in users" :key="user.id">
            <td>{{ user.id }}</td>
            <td>{{ user.name }}</td>
            <td>{{ user.email }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const users = ref([])
const loading = ref(true)
const error = ref(null)

// 模拟 API 请求
async function fetchUsers() {
  try {
    console.log('📊 开始获取数据...')
    
    // 模拟网络延迟
    await new Promise(resolve => setTimeout(resolve, 1500))
    
    // 模拟数据
    users.value = [
      { id: 1, name: '张三', email: 'zhangsan@example.com' },
      { id: 2, name: '李四', email: 'lisi@example.com' },
      { id: 3, name: '王五', email: 'wangwu@example.com' }
    ]
    
    console.log('✅ 数据获取成功')
  } catch (e) {
    console.error('❌ 数据获取失败:', e)
    error.value = e.message
  } finally {
    loading.value = false
  }
}

onMounted(() => {
  // 组件挂载后获取数据
  fetchUsers()
})
</script>

<style scoped>
.data-fetch-demo {
  background: white;
  border: 2px solid #e0e0e0;
  border-radius: 8px;
  overflow: hidden;
}

.data-fetch-demo h4 {
  padding: 15px 20px;
  background: #f5f5f5;
  color: #667eea;
  margin: 0;
  border-bottom: 1px solid #e0e0e0;
}

table {
  width: 100%;
  border-collapse: collapse;
}

th {
  background: #f9f9f9;
  padding: 12px;
  text-align: left;
  font-weight: 600;
  color: #667eea;
  border-bottom: 2px solid #e0e0e0;
}

td {
  padding: 12px;
  border-bottom: 1px solid #f0f0f0;
}

tr:last-child td {
  border-bottom: none;
}

tr:hover {
  background: #f9f9f9;
}

/* 加载动画 */
.spinner {
  width: 40px;
  height: 40px;
  border: 4px solid #f0f0f0;
  border-top-color: #667eea;
  border-radius: 50%;
  animation: spin 1s linear infinite;
  margin: 0 auto;
}

@keyframes spin {
  to { transform: rotate(360deg); }
}
</style>

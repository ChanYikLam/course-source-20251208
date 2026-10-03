<template>
  <div>
    <h2 class="demo-title">Props 验证与默认值</h2>

    <!-- 演示 1: 基础类型验证 -->
    <div class="example-section">
      <h3>✅ 演示 1: 基础类型验证</h3>
      <p>传递符合类型要求的 Props（打开控制台查看警告）</p>
      
      <div style="margin-top: 15px;">
        <UserCard
          title="张三的个人资料"
          :age="25"
          :isActive="true"
        />
      </div>

      <div style="margin-top: 15px; padding: 10px; background: #fff3cd; border-radius: 4px;">
        <strong>💡 提示：</strong>尝试传递错误类型会在控制台看到警告
      </div>
    </div>

    <!-- 演示 2: 必填项和默认值 -->
    <div class="example-section">
      <h3>📋 演示 2: 必填项和默认值</h3>
      
      <div style="margin-top: 15px;">
        <h4>使用默认值的组件：</h4>
        <ProductCard
          name="iPhone 15 Pro"
          :price="7999"
        />
      </div>

      <div style="margin-top: 15px;">
        <h4>自定义所有属性：</h4>
        <ProductCard
          name="MacBook Pro"
          :price="12999"
          category="电子产品"
          :inStock="false"
        />
      </div>
    </div>

    <!-- 演示 3: 对象/数组默认值 -->
    <div class="example-section">
      <h3>🎨 演示 3: 对象/数组默认值（工厂函数）</h3>
      
      <div style="margin-top: 15px;">
        <h4>使用默认配置：</h4>
        <ConfigPanel />
      </div>

      <div style="margin-top: 15px;">
        <h4>自定义配置：</h4>
        <ConfigPanel :options="customOptions" />
      </div>
    </div>

    <!-- 演示 4: 自定义验证器 -->
    <div class="example-section">
      <h3>🔍 演示 4: 自定义验证器</h3>
      
      <div style="margin-top: 15px;">
        <StatusBadge status="success" />
        <StatusBadge status="warning" />
        <StatusBadge status="error" />
      </div>

      <div style="margin-top: 15px; padding: 10px; background: #fff3cd; border-radius: 4px;">
        <strong>💡 提示：</strong>尝试传递 status="invalid" 会触发验证失败警告
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import UserCard from './props-components/UserCard.vue'
import ProductCard from './props-components/ProductCard.vue'
import ConfigPanel from './props-components/ConfigPanel.vue'
import StatusBadge from './props-components/StatusBadge.vue'

// 自定义配置对象
const customOptions = ref({
  theme: 'dark',
  language: 'en',
  notifications: false
})
</script>

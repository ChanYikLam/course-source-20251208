<template>
  <div>
    <h2 class="demo-title">v-model 在组件上的使用</h2>

    <!-- 演示 1: 传统写法（modelValue + update:modelValue） -->
    <div class="example-section">
      <h3>📝 演示 1: 传统 v-model 写法</h3>
      <p>使用 modelValue prop 和 update:modelValue 事件实现双向绑定</p>
      
      <div style="margin-top: 15px;">
        <CustomInput v-model="message1" placeholder="请输入内容..." />
        <p style="margin-top: 10px;">父组件的值: <strong>{{ message1 }}</strong></p>
      </div>

      <div style="margin-top: 15px; padding: 10px; background: #e7f3ff; border-radius: 4px;">
        <code>v-model="message"</code> 等价于<br>
        <code>:modelValue="message" @update:modelValue="message = $event"</code>
      </div>
    </div>

    <!-- 演示 2: defineModel 新写法（Vue 3.4+） -->
    <div class="example-section">
      <h3>✨ 演示 2: defineModel 新写法（推荐）</h3>
      <p>Vue 3.4+ 提供的更简洁的写法</p>
      
      <div style="margin-top: 15px;">
        <ModernInput v-model="message2" placeholder="使用 defineModel..." />
        <p style="margin-top: 10px;">父组件的值: <strong>{{ message2 }}</strong></p>
      </div>

      <div style="margin-top: 15px; padding: 10px; background: #d4edda; border-radius: 4px;">
        <strong>💡 新写法优势：</strong>子组件中直接使用 <code>const model = defineModel()</code><br>
        无需手动定义 props 和 emit，代码更简洁！
      </div>
    </div>

    <!-- 演示 3: 多个 v-model 绑定 -->
    <div class="example-section">
      <h3>🔗 演示 3: 多个 v-model 绑定</h3>
      <p>一个组件可以有多个 v-model</p>
      
      <div style="margin-top: 15px;">
        <UserForm
          v-model:firstName="firstName"
          v-model:lastName="lastName"
          v-model:email="email"
        />
        
        <div style="margin-top: 15px; padding: 15px; background: #f9f9f9; border-radius: 4px;">
          <h4>表单数据：</h4>
          <p>姓: <strong>{{ lastName }}</strong></p>
          <p>名: <strong>{{ firstName }}</strong></p>
          <p>邮箱: <strong>{{ email }}</strong></p>
        </div>
      </div>
    </div>

    <!-- 演示 4: 带修饰符的 v-model -->
    <div class="example-section">
      <h3>🎯 演示 4: v-model 修饰符</h3>
      
      <div style="margin-top: 15px;">
        <h4>普通输入：</h4>
        <CustomInput v-model="text1" />
        <p>值: {{ text1 }}</p>
      </div>

      <div style="margin-top: 15px;">
        <h4>自动去除首尾空格（.trim 修饰符）：</h4>
        <CustomInput v-model.trim="text2" />
        <p>值: "{{ text2 }}" (长度: {{ text2.length }})</p>
      </div>

      <div style="margin-top: 15px; padding: 10px; background: #fff3cd; border-radius: 4px;">
        <strong>💡 提示：</strong>v-model 支持 .trim、.number、.lazy 等修饰符
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import CustomInput from './vmodel-components/CustomInput.vue'
import ModernInput from './vmodel-components/ModernInput.vue'
import UserForm from './vmodel-components/UserForm.vue'

// 演示 1 和 2 的数据
const message1 = ref('')
const message2 = ref('')

// 演示 3 的数据
const firstName = ref('三')
const lastName = ref('张')
const email = ref('zhangsan@example.com')

// 演示 4 的数据
const text1 = ref('')
const text2 = ref('')
</script>

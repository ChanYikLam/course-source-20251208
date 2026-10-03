<template>
  <div>
    <h2 class="demo-title">插槽 Slots 演示</h2>

    <!-- 演示 1: 默认插槽 -->
    <div class="example-section">
      <h3>📦 演示 1: 默认插槽</h3>
      <p>父组件可以向子组件传递任意内容</p>
      
      <div style="margin-top: 15px;">
        <SimpleCard>
          <h3>这是卡片标题</h3>
          <p>这是卡片的内容，可以是任意 HTML 元素</p>
          <button class="btn">操作按钮</button>
        </SimpleCard>
      </div>

      <div style="margin-top: 15px;">
        <SimpleCard>
          <img src="https://picx.gdmuna.com/p/icons/gdmu-na/base/gdmuna-logo_gradient.svg" 
               style="width: 150px; border-radius: 4px;" />
          <p style="margin-top: 10px;">卡片中也可以放图片！</p>
        </SimpleCard>
      </div>
    </div>

    <!-- 演示 2: 具名插槽 -->
    <div class="example-section">
      <h3>🏷️ 演示 2: 具名插槽</h3>
      <p>一个组件可以有多个插槽位置</p>
      
      <div style="margin-top: 15px;">
        <PageLayout>
          <template #header>
            <h2 style="color: #667eea;">页面标题</h2>
            <p style="color: #999;">这是页面的描述信息</p>
          </template>
          
          <!-- 默认插槽内容 -->
          <p>这是页面的主要内容区域...</p>
          <p>可以放置任意内容</p>
          
          <template #footer>
            <button class="btn">保存</button>
            <button class="btn btn-secondary">取消</button>
          </template>
        </PageLayout>
      </div>
    </div>

    <!-- 演示 3: 作用域插槽 -->
    <div class="example-section">
      <h3>🔗 演示 3: 作用域插槽</h3>
      <p>子组件可以向插槽传递数据</p>
      
      <div style="margin-top: 15px;">
        <h4>用户列表（默认样式）：</h4>
        <UserList>
          <template #default="{ user, index }">
            <span>{{ index + 1 }}. {{ user.name }}</span>
            <span v-if="user.role === 'admin'" class="badge">管理员</span>
          </template>
        </UserList>
      </div>

      <div style="margin-top: 15px;">
        <h4>用户列表（自定义样式）：</h4>
        <UserList>
          <template #default="{ user, index }">
            <div style="display: flex; align-items: center; gap: 10px;">
              <span style="background: #667eea; color: white; width: 24px; height: 24px; 
                           border-radius: 50%; display: flex; align-items: center; 
                           justify-content: center; font-size: 12px;">
                {{ index + 1 }}
              </span>
              <span style="font-weight: 600;">{{ user.name }}</span>
              <span style="color: #999; font-size: 12px;">({{ user.role }})</span>
            </div>
          </template>
        </UserList>
      </div>
    </div>

    <!-- 演示 4: 后备内容（默认内容） -->
    <div class="example-section">
      <h3>🎯 演示 4: 插槽后备内容</h3>
      <p>插槽可以提供默认内容，如果父组件没有传递内容则显示默认内容</p>
      
      <div style="margin-top: 15px;">
        <h4>使用默认按钮文字：</h4>
        <SubmitButton />
      </div>

      <div style="margin-top: 15px;">
        <h4>自定义按钮文字：</h4>
        <SubmitButton>
          <span style="font-size: 16px;">✅ 确认提交</span>
        </SubmitButton>
      </div>
    </div>

    <!-- 演示 5: 动态插槽名 -->
    <div class="example-section">
      <h3>⚡ 演示 5: 动态插槽名</h3>
      <p>插槽名可以是动态的</p>
      
      <div style="margin-top: 15px;">
        <label>
          选择插槽位置:
          <select v-model="dynamicSlotName" style="margin-left: 10px; padding: 5px;">
            <option value="header">Header</option>
            <option value="footer">Footer</option>
          </select>
        </label>
      </div>

      <div style="margin-top: 15px;">
        <PageLayout>
          <template #[dynamicSlotName]>
            <div style="padding: 15px; background: #d4edda; border-radius: 4px; color: #155724;">
              ✨ 我在 {{ dynamicSlotName }} 插槽中！
            </div>
          </template>
          
          <p>主要内容区域</p>
        </PageLayout>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import SimpleCard from './slots-components/SimpleCard.vue'
import PageLayout from './slots-components/PageLayout.vue'
import UserList from './slots-components/UserList.vue'
import SubmitButton from './slots-components/SubmitButton.vue'

const dynamicSlotName = ref('header')
</script>

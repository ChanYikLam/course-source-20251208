<template>
  <div>
    <h2 class="demo-title">动态组件与 KeepAlive</h2>

    <!-- 演示 1: 基础动态组件 -->
    <div class="example-section">
      <h3>🔄 演示 1: 动态组件切换</h3>
      <p>使用 component :is 根据条件渲染不同组件</p>
      
      <div class="tabs">
        <button
          v-for="tab in tabs"
          :key="tab.name"
          :class="{ active: currentTab === tab.component }"
          @click="currentTab = tab.component"
          class="tab-button"
        >
          {{ tab.name }}
        </button>
      </div>

      <div style="margin-top: 15px;">
        <!-- 不使用 KeepAlive：每次切换都会销毁组件 -->
        <component :is="currentTab" />
      </div>

      <div style="margin-top: 15px; padding: 10px; background: #fff3cd; border-radius: 4px;">
        <strong>⚠️ 注意：</strong>切换 Tab 会销毁旧组件，输入的内容会丢失！
      </div>
    </div>

    <!-- 演示 2: KeepAlive 缓存组件 -->
    <div class="example-section">
      <h3>💾 演示 2: KeepAlive 保持状态</h3>
      <p>使用 KeepAlive 缓存组件，切换时不会销毁</p>
      
      <div class="tabs">
        <button
          v-for="tab in tabs"
          :key="tab.name"
          :class="{ active: currentTabCached === tab.component }"
          @click="currentTabCached = tab.component"
          class="tab-button"
        >
          {{ tab.name }}
        </button>
      </div>

      <div style="margin-top: 15px;">
        <!-- 使用 KeepAlive：组件会被缓存 -->
        <KeepAlive>
          <component :is="currentTabCached" />
        </KeepAlive>
      </div>

      <div style="margin-top: 15px; padding: 10px; background: #d4edda; border-radius: 4px;">
        <strong>✅ 好处：</strong>输入的内容会保留！组件状态不会丢失
      </div>
    </div>

    <!-- 演示 3: KeepAlive include/exclude -->
    <div class="example-section">
      <h3>🎯 演示 3: 选择性缓存</h3>
      <p>只缓存「购物车」，其他 Tab 不缓存</p>
      
      <div class="tabs">
        <button
          v-for="tab in tabs"
          :key="tab.name"
          :class="{ active: currentTabSelective === tab.component }"
          @click="currentTabSelective = tab.component"
          class="tab-button"
        >
          {{ tab.name }}
        </button>
      </div>

      <div style="margin-top: 15px;">
        <!-- include 只缓存指定组件 -->
        <KeepAlive include="TabCart">
          <component :is="currentTabSelective" />
        </KeepAlive>
      </div>

      <div style="margin-top: 15px; padding: 10px; background: #e7f3ff; border-radius: 4px;">
        <strong>💡 说明：</strong>只有购物车会保持状态，首页和个人中心切换时会重置
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, shallowRef } from 'vue'
import TabHome from './dynamic-components/TabHome.vue'
import TabCart from './dynamic-components/TabCart.vue'
import TabProfile from './dynamic-components/TabProfile.vue'

const tabs = [
  { name: '🏠 首页', component: TabHome },
  { name: '🛒 购物车', component: TabCart },
  { name: '👤 个人中心', component: TabProfile }
]

// 演示 1: 不缓存
const currentTab = shallowRef(TabHome)

// 演示 2: 全部缓存
const currentTabCached = shallowRef(TabHome)

// 演示 3: 选择性缓存
const currentTabSelective = shallowRef(TabHome)
</script>

<style scoped>
.tabs {
  display: flex;
  gap: 10px;
  border-bottom: 2px solid #e0e0e0;
  padding-bottom: 10px;
}

.tab-button {
  padding: 10px 20px;
  border: none;
  background: #f5f5f5;
  border-radius: 6px 6px 0 0;
  cursor: pointer;
  font-size: 14px;
  transition: all 0.3s;
}

.tab-button:hover {
  background: #e0e0e0;
}

.tab-button.active {
  background: #667eea;
  color: white;
}
</style>

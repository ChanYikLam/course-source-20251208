<template>
  <div>
    <h2 class="demo-title">组件生命周期钩子</h2>

    <!-- 演示 1: 基础生命周期流程 -->
    <div class="example-section">
      <h3>⏱️ 演示 1: 生命周期流程（打开控制台查看）</h3>
      <p>点击按钮显示/隐藏组件，观察控制台输出的生命周期钩子</p>
      
      <div style="margin-top: 15px;">
        <button class="btn" @click="showBasicDemo = !showBasicDemo">
          {{ showBasicDemo ? '隐藏组件' : '显示组件' }}
        </button>
        <button class="btn btn-secondary" @click="counter++" v-if="showBasicDemo" style="margin-left: 10px;">
          触发更新 ({{ counter }})
        </button>
      </div>

      <div v-if="showBasicDemo" style="margin-top: 15px;">
        <LifecycleBasic :counter="counter" />
      </div>

      <div style="margin-top: 15px; padding: 10px; background: #e7f3ff; border-radius: 4px;">
        <strong>💡 观察顺序：</strong><br>
        创建 → onMounted → 数据变化 → onUpdated → 销毁 → onUnmounted
      </div>
    </div>

    <!-- 演示 2: 实际场景 - 定时器 -->
    <div class="example-section">
      <h3>⏰ 演示 2: 定时器（必须清理）</h3>
      <p>使用 onMounted 启动定时器，onUnmounted 清理定时器</p>
      
      <div style="margin-top: 15px;">
        <button class="btn" @click="showTimer = !showTimer">
          {{ showTimer ? '停止计时器' : '启动计时器' }}
        </button>
      </div>

      <div v-if="showTimer" style="margin-top: 15px;">
        <TimerDemo />
      </div>

      <div style="margin-top: 15px; padding: 10px; background: #fff3cd; border-radius: 4px;">
        <strong>⚠️ 重要：</strong>必须在 onUnmounted 中清理定时器，否则会内存泄漏！
      </div>
    </div>

    <!-- 演示 3: 实际场景 - 事件监听 -->
    <div class="example-section">
      <h3>📏 演示 3: 窗口大小监听</h3>
      <p>使用 onMounted 添加全局事件监听，onUnmounted 移除监听</p>
      
      <div style="margin-top: 15px;">
        <button class="btn" @click="showResize = !showResize">
          {{ showResize ? '停止监听' : '开始监听' }}
        </button>
      </div>

      <div v-if="showResize" style="margin-top: 15px;">
        <WindowSizeDemo />
      </div>
    </div>

    <!-- 演示 4: 实际场景 - DOM 操作 -->
    <div class="example-section">
      <h3>🎯 演示 4: DOM 操作（自动聚焦）</h3>
      <p>使用 onMounted 在组件挂载后操作 DOM</p>
      
      <div style="margin-top: 15px;">
        <button class="btn" @click="showAutoFocus = !showAutoFocus">
          {{ showAutoFocus ? '隐藏输入框' : '显示输入框' }}
        </button>
      </div>

      <div v-if="showAutoFocus" style="margin-top: 15px;">
        <AutoFocusInput />
      </div>
    </div>

    <!-- 演示 5: 实际场景 - 数据获取 -->
    <div class="example-section">
      <h3>📊 演示 5: 获取数据（模拟 API 请求）</h3>
      <p>使用 onMounted 在组件挂载后获取数据</p>
      
      <div style="margin-top: 15px;">
        <button class="btn" @click="showDataFetch = !showDataFetch">
          {{ showDataFetch ? '隐藏数据' : '加载数据' }}
        </button>
      </div>

      <div v-if="showDataFetch" style="margin-top: 15px;">
        <DataFetchDemo />
      </div>
    </div>

    <!-- 生命周期图示 -->
    <div class="example-section">
      <h3>📚 生命周期钩子速查</h3>
      <table>
        <thead>
          <tr>
            <th>钩子函数</th>
            <th>触发时机</th>
            <th>常用场景</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td><code>onMounted</code></td>
            <td>组件挂载完成</td>
            <td>获取数据、操作 DOM、启动定时器</td>
          </tr>
          <tr>
            <td><code>onUpdated</code></td>
            <td>数据更新后</td>
            <td>响应数据变化、第三方库更新</td>
          </tr>
          <tr>
            <td><code>onUnmounted</code></td>
            <td>组件卸载前</td>
            <td>清理定时器、移除事件监听</td>
          </tr>
          <tr>
            <td><code>onBeforeMount</code></td>
            <td>挂载前</td>
            <td>很少使用</td>
          </tr>
          <tr>
            <td><code>onBeforeUpdate</code></td>
            <td>更新前</td>
            <td>很少使用</td>
          </tr>
          <tr>
            <td><code>onBeforeUnmount</code></td>
            <td>卸载前</td>
            <td>清理工作（优先用 onUnmounted）</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import LifecycleBasic from './lifecycle-components/LifecycleBasic.vue'
import TimerDemo from './lifecycle-components/TimerDemo.vue'
import WindowSizeDemo from './lifecycle-components/WindowSizeDemo.vue'
import AutoFocusInput from './lifecycle-components/AutoFocusInput.vue'
import DataFetchDemo from './lifecycle-components/DataFetchDemo.vue'

const showBasicDemo = ref(false)
const counter = ref(0)
const showTimer = ref(false)
const showResize = ref(false)
const showAutoFocus = ref(false)
const showDataFetch = ref(false)
</script>

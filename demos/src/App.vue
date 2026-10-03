<template>
  <div>
    <!-- 导航栏 -->
    <nav class="demo-nav">
      <h1>📚 Vue 3 组件化进阶 - 课堂演示</h1>
      <div class="demo-nav-buttons">
        <button
          v-for="demo in demos"
          :key="demo.id"
          :class="{ active: currentDemo === demo.id }"
          @click="currentDemo = demo.id"
        >
          {{ demo.title }}
        </button>
      </div>
    </nav>

    <!-- 演示内容区域 -->
    <div class="demo-container">
      <component :is="currentComponent" />
    </div>
  </div>
</template>

<script setup>
import { ref, shallowRef, computed } from 'vue'

// 引入所有演示组件
import Demo1PropsValidation from './demos/Demo1PropsValidation.vue'
import Demo2VModel from './demos/Demo2VModel.vue'
import Demo3Slots from './demos/Demo3Slots.vue'
import Demo4Lifecycle from './demos/Demo4Lifecycle.vue'
import Demo5ProvideInject from './demos/Demo5ProvideInject.vue'
import Demo6DynamicComponents from './demos/Demo6DynamicComponents.vue'
import Demo7Teleport from './demos/Demo7Teleport.vue'
import Demo8Computed from './demos/Demo8Computed.vue'
import Demo9Watch from './demos/Demo9Watch.vue'
import Demo10TemplateRefs from './demos/Demo10TemplateRefs.vue'

// 演示列表配置
const demos = [
  { id: 'props', title: '1️⃣ Props 验证', component: Demo1PropsValidation },
  { id: 'vmodel', title: '2️⃣ v-model 组件', component: Demo2VModel },
  { id: 'slots', title: '3️⃣ 插槽 Slots', component: Demo3Slots },
  { id: 'computed', title: '4️⃣ computed 计算', component: Demo8Computed },
  { id: 'watch', title: '5️⃣ watch 侦听', component: Demo9Watch },
  { id: 'refs', title: '6️⃣ 模板引用', component: Demo10TemplateRefs },
  { id: 'lifecycle', title: '7️⃣ 生命周期', component: Demo4Lifecycle },
  { id: 'provide', title: '8️⃣ provide/inject', component: Demo5ProvideInject },
  { id: 'dynamic', title: '9️⃣ 动态组件', component: Demo6DynamicComponents },
  { id: 'teleport', title: '🔟 Teleport', component: Demo7Teleport }
]

// 当前选中的演示
const currentDemo = ref('props')

// 当前显示的组件
const currentComponent = computed(() => {
  const demo = demos.find(d => d.id === currentDemo.value)
  return demo ? demo.component : null
})
</script>

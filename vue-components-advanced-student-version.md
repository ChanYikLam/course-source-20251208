# Vue 3 组件化进阶 — 学生学习文档

---

## 📚 学习目标

完成这节课后，你应该能够：

- [ ] 使用 Props 验证和默认值增强组件健壮性
- [ ] 在组件上使用 `v-model` 实现双向绑定
- [ ] 使用插槽（Slot）创建灵活的可复用组件
- [ ] 使用 `computed` 创建计算属性并理解缓存机制
- [ ] 使用 `watch` 侦听数据变化并执行副作用
- [ ] 使用模板引用 `ref` 访问 DOM 元素和组件实例
- [ ] 理解组件生命周期并正确使用钩子函数
- [ ] 使用 `provide` / `inject` 解决深层组件通信
- [ ] 使用动态组件和 `<KeepAlive>` 优化用户体验

---

## 🎯 核心概念速览

| 概念 | 一句话解释 |
|------|-----------|
| **Props 验证** | 对传入的 Props 进行类型检查和默认值设置 |
| **v-model 组件** | 让自定义组件支持双向数据绑定 |
| **插槽 Slot** | 让父组件向子组件传递模板内容 |
| **computed** | 基于依赖缓存的计算属性 |
| **watch** | 侦听响应式数据变化并执行副作用 |
| **模板引用** | 使用 ref 访问 DOM 元素或组件实例 |
| **生命周期** | 组件从创建到销毁的各个阶段 |
| **provide/inject** | 祖先组件向所有后代组件传递数据 |
| **动态组件** | 根据条件切换显示不同的组件 |

---

## 📖 第一部分：组件通信深入

### 1.1 Props 高级用法

上节课我们学习了基础的 Props 传递，现在来看更完整的用法。

#### Props 类型验证

```html
<script setup>
// 使用 defineProps 定义 Props 并添加验证
const props = defineProps({
    // 基础类型检查
    title: String,
    count: Number,
    isActive: Boolean,
    
    // 多种类型
    id: [String, Number],
    
    // 必填项
    username: {
        type: String,
        required: true
    },
    
    // 带默认值
    size: {
        type: String,
        default: 'medium'
    },
    
    // 对象/数组默认值必须用工厂函数
    options: {
        type: Object,
        default: () => ({ color: 'blue' })
    },
    
    // 自定义验证函数
    status: {
        type: String,
        validator: (value) => {
            return ['pending', 'success', 'error'].includes(value)
        }
    }
})
</script>
```

**类型对照表**：

| 类型 | 说明 | 示例 |
|------|------|------|
| `String` | 字符串 | `"hello"` |
| `Number` | 数字 | `42` |
| `Boolean` | 布尔值 | `true` |
| `Array` | 数组 | `[1, 2, 3]` |
| `Object` | 对象 | `{ name: '张三' }` |
| `Function` | 函数 | `() => {}` |
| `Date` | 日期对象 | `new Date()` |

#### 使用 TypeScript 风格（推荐）

```html
<script setup lang="ts">
// 更简洁的写法，类型更明确
interface Props {
    title: string
    count?: number        // ? 表示可选
    items: string[]
    user: {
        name: string
        age: number
    }
}

const props = withDefaults(defineProps<Props>(), {
    count: 0,             // 默认值
    items: () => []       // 数组/对象默认值用工厂函数
})
</script>
```

---

### 1.2 v-model 在组件上的使用

在原生 HTML 元素上，`v-model` 是双向绑定的语法糖：

```html
<!-- 原生 input -->
<input v-model="searchText" />

<!-- 等价于 -->
<input :value="searchText" @input="searchText = $event.target.value" />
```

在**自定义组件**上使用 `v-model`，原理类似：

```html
<!-- 父组件使用 -->
<CustomInput v-model="message" />

<!-- 等价于 -->
<CustomInput :modelValue="message" @update:modelValue="message = $event" />
```

#### 子组件实现 v-model

```html
<!-- CustomInput.vue -->
<template>
    <input
        :value="modelValue"
        @input="$emit('update:modelValue', $event.target.value)"
    />
</template>

<script setup>
defineProps({
    modelValue: String
})

defineEmits(['update:modelValue'])
</script>
```

#### 使用 defineModel（Vue 3.4+ 推荐）

Vue 3.4 引入了更简洁的 `defineModel`：

```html
<!-- CustomInput.vue（新写法） -->
<template>
    <input v-model="model" />
</template>

<script setup>
// defineModel 自动处理 props 和 emit
const model = defineModel()
</script>
```

就这么简单！`defineModel()` 返回一个 ref，可以直接在子组件中读写。

#### 多个 v-model 绑定

```html
<!-- 父组件 -->
<UserForm
    v-model:firstName="first"
    v-model:lastName="last"
/>

<!-- UserForm.vue -->
<template>
    <input v-model="firstName" placeholder="名" />
    <input v-model="lastName" placeholder="姓" />
</template>

<script setup>
const firstName = defineModel('firstName')
const lastName = defineModel('lastName')
</script>
```

---

### 1.3 透传属性 $attrs

当父组件传递的属性/事件没有被子组件声明为 Props 或 Emits 时，它们会被"透传"。

```html
<!-- 父组件 -->
<MyButton class="large" @click="handleClick">
    点击我
</MyButton>

<!-- MyButton.vue -->
<template>
    <!-- class 和 @click 会自动透传到根元素 -->
    <button>
        <slot></slot>
    </button>
</template>

<!-- 渲染结果 -->
<button class="large">点击我</button>
```

#### 禁用自动透传

```html
<script setup>
// 禁用自动透传，手动控制
defineOptions({
    inheritAttrs: false
})
</script>

<template>
    <div class="wrapper">
        <!-- 手动绑定 $attrs 到指定元素 -->
        <button v-bind="$attrs">
            <slot></slot>
        </button>
    </div>
</template>
```

---

## 📖 第二部分：插槽 Slots

### 2.1 为什么需要插槽？

Props 只能传递**数据**，但有时我们需要传递**模板内容**（HTML 结构）。

<pre>
没有插槽：
┌─────────────────┐
│   Card 组件      │  ← 内容固定，不灵活
│  ┌───────────┐  │
│  │ 固定内容   │  │
│  └───────────┘  │
└─────────────────┘

有了插槽：
┌─────────────────┐
│   Card 组件      │  ← 外壳固定，内容由父组件决定
│  ┌───────────┐  │
│  │   slot    │  │  ← 父组件可以放任何内容
│  └───────────┘  │
└─────────────────┘
</pre>

### 2.2 默认插槽

```html
<!-- Card.vue（子组件） -->
<template>
    <div class="card">
        <div class="card-body">
            <!-- 插槽出口：父组件的内容会渲染到这里 -->
            <slot></slot>
        </div>
    </div>
</template>

<style scoped>
.card {
    border: 1px solid #e0e0e0;
    border-radius: 8px;
    padding: 16px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}
</style>
```

```html
<!-- 父组件使用 -->
<template>
    <Card>
        <!-- 这里的内容会替换 <slot></slot> -->
        <h3>卡片标题</h3>
        <p>这是卡片的内容，可以是任意 HTML</p>
        <button>操作按钮</button>
    </Card>
</template>
```

#### 默认内容（后备内容）

```html
<template>
    <button class="btn">
        <slot>
            <!-- 如果父组件没有提供内容，显示默认内容 -->
            默认按钮文字
        </slot>
    </button>
</template>
```

```html
<!-- 使用时 -->
<MyButton></MyButton>          <!-- 显示：默认按钮文字 -->
<MyButton>点击提交</MyButton>   <!-- 显示：点击提交 -->
```

---

### 2.3 具名插槽

当组件需要多个插槽位置时，使用**具名插槽**：

```html
<!-- PageLayout.vue -->
<template>
    <div class="page">
        <header>
            <slot name="header"></slot>
        </header>
        
        <main>
            <slot></slot>  <!-- 默认插槽，等价于 name="default" -->
        </main>
        
        <footer>
            <slot name="footer"></slot>
        </footer>
    </div>
</template>
```

```html
<!-- 父组件使用 -->
<template>
    <PageLayout>
        <!-- 使用 v-slot:名称 或简写 #名称 -->
        <template #header>
            <h1>页面标题</h1>
            <nav>导航栏</nav>
        </template>
        
        <!-- 默认插槽内容 -->
        <p>这是页面的主要内容...</p>
        <p>可以有多个元素</p>
        
        <template #footer>
            <p>© 2025 版权所有</p>
        </template>
    </PageLayout>
</template>
```

**渲染结果**：

```html
<div class="page">
    <header>
        <h1>页面标题</h1>
        <nav>导航栏</nav>
    </header>
    <main>
        <p>这是页面的主要内容...</p>
        <p>可以有多个元素</p>
    </main>
    <footer>
        <p>© 2025 版权所有</p>
    </footer>
</div>
```

---

### 2.4 作用域插槽

有时候插槽内容需要访问**子组件的数据**。作用域插槽允许子组件向插槽传递数据。

```html
<!-- UserList.vue（子组件） -->
<template>
    <ul>
        <li v-for="user in users" :key="user.id">
            <!-- 通过 slot 向父组件传递数据 -->
            <slot :user="user" :index="index"></slot>
        </li>
    </ul>
</template>

<script setup>
import { ref } from 'vue'

const users = ref([
    { id: 1, name: '张三', role: 'admin' },
    { id: 2, name: '李四', role: 'user' },
    { id: 3, name: '王五', role: 'user' }
])
</script>
```

```html
<!-- 父组件使用 -->
<template>
    <UserList>
        <!-- 通过 v-slot 接收子组件传递的数据 -->
        <template #default="{ user, index }">
            <span>{{ index + 1 }}. {{ user.name }}</span>
            <span v-if="user.role === 'admin'" class="badge">管理员</span>
        </template>
    </UserList>
</template>
```

**理解作用域插槽**：

<pre>
┌─────────────────────────────────────┐
│  父组件                              │
│  ┌─────────────────────────────┐   │
│  │  <UserList>                  │   │
│  │    <template #default="props">│  │  ← 接收子组件的数据
│  │      {{ props.user.name }}   │   │
│  │    </template>               │   │
│  │  </UserList>                 │   │
│  └─────────────────────────────┘   │
└─────────────────────────────────────┘
                    ↑
          数据从子组件流向父组件
                    ↑
┌─────────────────────────────────────┐
│  子组件 UserList                     │
│  <slot :user="user"></slot>         │  ← 向插槽传递数据
└─────────────────────────────────────┘
</pre>

---

### 2.5 动态插槽名

插槽名可以是动态的，使用 JavaScript 表达式：

```html
<!-- 子组件：PageLayout.vue -->
<template>
    <div class="page">
        <header>
            <slot name="header"></slot>
        </header>
        
        <main>
            <slot></slot>
        </main>
        
        <footer>
            <slot name="footer"></slot>
        </footer>
    </div>
</template>
```

```html
<!-- 父组件使用动态插槽名 -->
<template>
    <div>
        <!-- 选择插槽位置 -->
        <select v-model="slotPosition">
            <option value="header">Header</option>
            <option value="footer">Footer</option>
        </select>
        
        <PageLayout>
            <!-- 使用动态插槽名：#[变量名] -->
            <template #[slotPosition]>
                <div class="highlight">
                    ✨ 我在 {{ slotPosition }} 位置
                </div>
            </template>
            
            <p>主要内容区域</p>
        </PageLayout>
    </div>
</template>

<script setup>
import { ref } from 'vue'
const slotPosition = ref('header')
</script>
```

**使用场景**：
- 根据用户选择动态改变内容位置
- 响应式布局需要动态调整插槽
- 根据设备类型（手机/电脑）切换插槽位置

**语法要点**：
- 使用 `#[变量名]` 或 `v-slot:[变量名]`
- 变量值必须是有效的插槽名（字符串）
- 可以与作用域插槽结合使用：`#[slotName]="slotProps"`

---

### ✏️ Task 1：使用插槽创建 Card 组件（20分钟）

**目标**：练习默认插槽和具名插槽

创建一个 `Card` 组件，支持以下插槽：
- `header` 插槽：卡片标题区域
- 默认插槽：卡片内容区域
- `footer` 插槽：卡片底部操作区域

**要求**：
- header 和 footer 是可选的
- 提供合理的默认样式
- 在 App.vue 中使用多个 Card 展示不同内容

**提示**：参考 2.3 节具名插槽的写法

---

## 📖 第三部分：响应式 API 深入

### 3.1 computed 计算属性

#### 什么是计算属性？

计算属性是**基于响应式依赖进行缓存的**计算值。只有当依赖的响应式数据变化时，计算属性才会重新计算。

```html
<script setup>
import { ref, computed } from 'vue'

const firstName = ref('张')
const lastName = ref('三')

// 计算属性：自动追踪依赖
const fullName = computed(() => {
    return firstName.value + lastName.value
})
</script>

<template>
    <p>全名: {{ fullName }}</p>
    <!-- 修改依赖时，fullName 会自动更新 -->
    <input v-model="firstName" />
    <input v-model="lastName" />
</template>
```

#### computed vs 方法

**方法**每次渲染都会执行，**计算属性**只在依赖变化时才重新计算：

```html
<script setup>
import { ref, computed } from 'vue'

const count = ref(0)

// 方法：每次调用都执行
function getDoubleByMethod() {
    console.log('方法被调用')
    return count.value * 2
}

// 计算属性：只在 count 变化时重新计算
const doubleByComputed = computed(() => {
    console.log('计算属性被计算')
    return count.value * 2
})
</script>

<template>
    <!-- 每次渲染都会执行 3 次 -->
    <p>{{ getDoubleByMethod() }}</p>
    <p>{{ getDoubleByMethod() }}</p>
    <p>{{ getDoubleByMethod() }}</p>
    
    <!-- 只计算一次，其他两次使用缓存 -->
    <p>{{ doubleByComputed }}</p>
    <p>{{ doubleByComputed }}</p>
    <p>{{ doubleByComputed }}</p>
</template>
```

#### 可写计算属性

计算属性默认是只读的，但也可以定义 getter 和 setter：

```html
<script setup>
import { ref, computed } from 'vue'

const firstName = ref('张')
const lastName = ref('三')

const fullName = computed({
    // getter
    get() {
        return firstName.value + lastName.value
    },
    // setter
    set(newValue) {
        // 假设格式是"姓名"
        firstName.value = newValue[0]
        lastName.value = newValue.slice(1)
    }
})
</script>

<template>
    <!-- 读取 -->
    <p>{{ fullName }}</p>
    
    <!-- 写入：会触发 setter -->
    <input v-model="fullName" />
</template>
```

#### 使用场景

| 场景 | 示例 |
|------|------|
| **过滤/排序列表** | 根据搜索关键词过滤商品列表 |
| **格式化显示** | 将时间戳格式化为日期字符串 |
| **组合数据** | 将多个响应式数据组合成一个 |
| **复杂计算** | 购物车总价、统计数据等 |

```html
<script setup>
import { ref, computed } from 'vue'

const products = ref([
    { id: 1, name: 'iPhone', price: 7999, count: 2 },
    { id: 2, name: 'iPad', price: 3999, count: 1 },
    { id: 3, name: 'MacBook', price: 12999, count: 1 }
])

// 计算总价
const totalPrice = computed(() => {
    return products.value.reduce((sum, item) => {
        return sum + item.price * item.count
    }, 0)
})

// 格式化显示
const formattedTotal = computed(() => {
    return '¥' + totalPrice.value.toLocaleString()
})
</script>

<template>
    <p>总计: {{ formattedTotal }}</p>
</template>
```

---

### 3.2 watch 侦听器

#### 基本用法

`watch` 用于在响应式数据变化时执行副作用（如 API 请求、日志记录等）：

```html
<script setup>
import { ref, watch } from 'vue'

const question = ref('')
const answer = ref('请输入问题...')

// 侦听 question 的变化
watch(question, (newValue, oldValue) => {
    console.log(`问题从 "${oldValue}" 变为 "${newValue}"`)
    
    if (newValue.includes('?')) {
        answer.value = '正在思考...'
        // 模拟 API 请求
        setTimeout(() => {
            answer.value = '这是一个好问题！'
        }, 1000)
    }
})
</script>

<template>
    <input v-model="question" placeholder="输入问题（以 ? 结尾）" />
    <p>{{ answer }}</p>
</template>
```

#### 深度侦听

侦听对象内部属性的变化：

```html
<script setup>
import { ref, watch } from 'vue'

const user = ref({
    name: '张三',
    profile: {
        age: 25,
        city: '北京'
    }
})

// 默认不会侦听对象内部变化
watch(user, (newValue) => {
    console.log('user 变化', newValue)
})

// 使用 deep: true 深度侦听
watch(user, (newValue) => {
    console.log('user 深度变化', newValue)
}, { deep: true })

// 只侦听特定属性
watch(() => user.value.profile.age, (newAge) => {
    console.log('年龄变为', newAge)
})
</script>
```

#### 立即执行

使用 `immediate: true` 让侦听器立即执行一次：

```html
<script setup>
import { ref, watch } from 'vue'

const userId = ref(1)

watch(userId, async (id) => {
    // 获取用户数据
    const response = await fetch(`/api/users/${id}`)
    // ...
}, { immediate: true })  // 组件挂载时立即执行
</script>
```

#### 侦听多个源

```html
<script setup>
import { ref, watch } from 'vue'

const firstName = ref('张')
const lastName = ref('三')

// 侦听多个响应式数据
watch([firstName, lastName], ([newFirst, newLast], [oldFirst, oldLast]) => {
    console.log(`姓名从 ${oldFirst}${oldLast} 变为 ${newFirst}${newLast}`)
})
</script>
```

#### watchEffect 自动追踪依赖

`watchEffect` 会自动追踪回调函数中使用的响应式依赖：

```html
<script setup>
import { ref, watchEffect } from 'vue'

const count = ref(0)
const doubled = ref(0)

// 自动追踪 count，不需要显式指定
watchEffect(() => {
    console.log('count 变化了:', count.value)
    doubled.value = count.value * 2
})
</script>
```

**watch vs watchEffect**：

| 特性 | watch | watchEffect |
|------|-------|-------------|
| **依赖声明** | 显式指定 | 自动追踪 |
| **访问旧值** | 可以 | 不可以 |
| **执行时机** | 默认懒执行 | 立即执行 |
| **适用场景** | 需要对比新旧值 | 简单的副作用 |

#### 停止侦听

```html
<script setup>
import { ref, watch } from 'vue'

const count = ref(0)

// watch 返回一个停止函数
const stopWatch = watch(count, (newValue) => {
    console.log(newValue)
    
    if (newValue >= 10) {
        stopWatch()  // 停止侦听
    }
})
</script>
```

---

### 3.3 模板引用 ref

#### 访问 DOM 元素

使用 `ref` 可以直接访问 DOM 元素：

```html
<script setup>
import { ref, onMounted } from 'vue'

// 创建 ref，初始值为 null
const inputRef = ref(null)

onMounted(() => {
    // 组件挂载后，ref.value 指向 DOM 元素
    inputRef.value.focus()
    console.log('输入框元素:', inputRef.value)
})
</script>

<template>
    <!-- 通过 ref 属性绑定 -->
    <input ref="inputRef" />
</template>
```

#### 访问子组件实例

```html
<!-- 父组件 -->
<script setup>
import { ref, onMounted } from 'vue'
import ChildComponent from './ChildComponent.vue'

const childRef = ref(null)

onMounted(() => {
    // 访问子组件的方法和数据
    childRef.value.childMethod()
    console.log(childRef.value.childData)
})
</script>

<template>
    <ChildComponent ref="childRef" />
</template>
```

```html
<!-- 子组件 ChildComponent.vue -->
<script setup>
import { ref } from 'vue'

const childData = ref('子组件数据')

function childMethod() {
    console.log('子组件方法被调用')
}

// 暴露给父组件
defineExpose({
    childData,
    childMethod
})
</script>
```

#### v-for 中的 ref

在 `v-for` 中使用 ref，Vue 会自动将元素收集到数组中：

```html
<script setup>
import { ref, onMounted } from 'vue'

const itemRefs = ref([])

onMounted(() => {
    console.log('所有项:', itemRefs.value)
    // itemRefs.value 是一个包含所有 li 元素的数组
})
</script>

<template>
    <ul>
        <!-- ✅ 推荐：直接写 ref 名称，Vue 自动收集到数组 -->
        <li v-for="item in 5" :key="item" ref="itemRefs">
            Item {{ item }}
        </li>
    </ul>
</template>
```

#### 注意事项

1. **ref 在模板渲染后才可用**：在 `onMounted` 或之后访问
2. **组件卸载后 ref 会被清空**：避免内存泄漏
3. **子组件需要 defineExpose**：默认情况下子组件不暴露任何内容

---

## 📖 第四部分：组件生命周期

### 4.1 什么是生命周期？

组件从创建到销毁会经历一系列阶段，Vue 在每个阶段提供**钩子函数**，让我们在特定时机执行代码。

<pre>
组件生命周期流程：

创建阶段
    │
    ▼
┌─────────────┐
│   setup()   │  ← 组合式 API 的入口
└─────────────┘
    │
    ▼
┌─────────────┐
│ onBeforeMount│  ← 挂载前
└─────────────┘
    │
    ▼
┌─────────────┐
│  onMounted  │  ← 挂载完成，DOM 已可用 ⭐
└─────────────┘
    │
    ▼
更新阶段（数据变化时）
    │
    ▼
┌─────────────┐
│onBeforeUpdate│  ← 更新前
└─────────────┘
    │
    ▼
┌─────────────┐
│  onUpdated  │  ← 更新完成
└─────────────┘
    │
    ▼
卸载阶段
    │
    ▼
┌─────────────┐
│onBeforeUnmount│  ← 卸载前
└─────────────┘
    │
    ▼
┌─────────────┐
│ onUnmounted │  ← 卸载完成 ⭐
└─────────────┘
</pre>

### 4.2 常用生命周期钩子

```html
<script setup>
import { ref, onMounted, onUnmounted, onUpdated } from 'vue'

const count = ref(0)

// 组件挂载完成后执行
// 常用于：获取数据、操作 DOM、初始化第三方库
onMounted(() => {
    console.log('组件已挂载')
    console.log('DOM 元素:', document.querySelector('.my-element'))
    
    // 示例：获取数据
    fetchData()
})

// 组件卸载时执行
// 常用于：清理定时器、取消订阅、移除事件监听
onUnmounted(() => {
    console.log('组件已卸载')
})

// 数据更新后执行
// 注意：尽量避免在这里修改数据，可能导致无限循环
onUpdated(() => {
    console.log('组件已更新，count =', count.value)
})

async function fetchData() {
    // 模拟 API 请求
    const response = await fetch('/api/data')
    // ...
}
</script>
```

### 4.3 实际使用场景

#### 场景 1：定时器

```html
<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const seconds = ref(0)
let timer = null

onMounted(() => {
    // 组件挂载后启动定时器
    timer = setInterval(() => {
        seconds.value++
    }, 1000)
})

onUnmounted(() => {
    // 组件卸载时清理定时器，防止内存泄漏！
    if (timer) {
        clearInterval(timer)
    }
})
</script>

<template>
    <p>已运行 {{ seconds }} 秒</p>
</template>
```

#### 场景 2：事件监听

```html
<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const windowWidth = ref(window.innerWidth)

function handleResize() {
    windowWidth.value = window.innerWidth
}

onMounted(() => {
    // 添加全局事件监听
    window.addEventListener('resize', handleResize)
})

onUnmounted(() => {
    // 移除事件监听，防止内存泄漏！
    window.removeEventListener('resize', handleResize)
})
</script>

<template>
    <p>窗口宽度: {{ windowWidth }}px</p>
</template>
```

#### 场景 3：DOM 操作

```html
<script setup>
import { ref, onMounted } from 'vue'

const inputRef = ref(null)

onMounted(() => {
    // 组件挂载后，自动聚焦输入框
    inputRef.value.focus()
})
</script>

<template>
    <input ref="inputRef" placeholder="自动聚焦" />
</template>
```

---

## 📖 第五部分：provide / inject

### 5.1 Props 逐级透传的问题

当组件层级很深时，通过 Props 一层层传递数据很繁琐：

<pre>
┌─────────────────────────────────┐
│  App（有数据 theme）             │
│  └─ Parent                      │
│      └─ Child                   │
│          └─ GrandChild          │
│              └─ DeepChild       │  ← 需要使用 theme
└─────────────────────────────────┘

使用 Props：
App → theme → Parent → theme → Child → theme → GrandChild → theme → DeepChild

每一层都要声明 Props，即使中间层并不需要这个数据！
</pre>

### 5.2 provide / inject 解决方案

`provide` / `inject` 允许祖先组件直接向所有后代组件传递数据：

<pre>
┌─────────────────────────────────┐
│  App                            │
│    provide('theme', 'dark') ────┼──────────────────┐
│  └─ Parent                      │                   │
│      └─ Child                   │                   │
│          └─ GrandChild          │                   │
│              └─ DeepChild       │                   │
│                  inject('theme')│ ← 直接获取 ───────┘
└─────────────────────────────────┘
</pre>

#### 基本用法

```html
<!-- 祖先组件 App.vue -->
<script setup>
import { ref, provide } from 'vue'

const theme = ref('light')
const toggleTheme = () => {
    theme.value = theme.value === 'light' ? 'dark' : 'light'
}

// 提供数据
provide('theme', theme)          // 提供响应式数据
provide('toggleTheme', toggleTheme)  // 也可以提供函数
</script>
```

```html
<!-- 任意深度的后代组件 -->
<script setup>
import { inject } from 'vue'

// 注入数据
const theme = inject('theme')
const toggleTheme = inject('toggleTheme')

// 可以提供默认值
const language = inject('language', 'zh-CN')
</script>

<template>
    <div :class="theme">
        当前主题: {{ theme }}
        <button @click="toggleTheme">切换主题</button>
    </div>
</template>
```

### 5.3 使用 Symbol 作为 key

为避免命名冲突，推荐使用 Symbol：

```js
// keys.js
export const themeKey = Symbol('theme')
export const userKey = Symbol('user')
```

```html
<!-- 提供方 -->
<script setup>
import { provide } from 'vue'
import { themeKey } from './keys'

provide(themeKey, 'dark')
</script>
```

```html
<!-- 注入方 -->
<script setup>
import { inject } from 'vue'
import { themeKey } from './keys'

const theme = inject(themeKey)
</script>
```

### 5.4 最佳实践

1. **保持数据单向流动**：如果需要后代修改数据，provide 一个方法而不是让后代直接修改

```html
<!-- ✅ 推荐：提供方法 -->
<script setup>
import { ref, provide } from 'vue'

const count = ref(0)

// 提供数据和修改方法
provide('count', {
    count,
    increment: () => count.value++,
    decrement: () => count.value--
})
</script>
```

2. **使用 readonly 保护数据**

```html
<script setup>
import { ref, provide, readonly } from 'vue'

const user = ref({ name: '张三' })

// 后代只能读取，不能修改
provide('user', readonly(user))
</script>
```

---

## 📖 第六部分：动态组件与异步组件

### 6.1 动态组件

使用 `<component :is="">` 根据条件切换组件：

```html
<script setup>
import { ref, shallowRef } from 'vue'
import TabHome from './TabHome.vue'
import TabProfile from './TabProfile.vue'
import TabSettings from './TabSettings.vue'

// 使用 shallowRef 存储组件引用（性能优化）
const currentTab = shallowRef(TabHome)

const tabs = [
    { name: '首页', component: TabHome },
    { name: '个人', component: TabProfile },
    { name: '设置', component: TabSettings }
]
</script>

<template>
    <div class="tabs">
        <button
            v-for="tab in tabs"
            :key="tab.name"
            :class="{ active: currentTab === tab.component }"
            @click="currentTab = tab.component"
        >
            {{ tab.name }}
        </button>
    </div>
    
    <!-- 动态组件 -->
    <component :is="currentTab" />
</template>
```

### 6.2 KeepAlive 缓存组件状态

默认情况下，切换组件时旧组件会被销毁。使用 `<KeepAlive>` 可以缓存组件状态：

```html
<template>
    <!-- 包裹在 KeepAlive 中的组件会被缓存 -->
    <KeepAlive>
        <component :is="currentTab" />
    </KeepAlive>
</template>
```

**缓存效果**：

```
不使用 KeepAlive：
Tab1（有输入内容） → 切换到 Tab2 → 切回 Tab1 → 输入内容丢失 ❌

使用 KeepAlive：
Tab1（有输入内容） → 切换到 Tab2 → 切回 Tab1 → 输入内容保留 ✅
```

#### KeepAlive 的选项

```html
<!-- 只缓存指定组件 -->
<KeepAlive include="TabHome,TabProfile">
    <component :is="currentTab" />
</KeepAlive>

<!-- 排除指定组件 -->
<KeepAlive exclude="TabSettings">
    <component :is="currentTab" />
</KeepAlive>

<!-- 最多缓存 5 个组件 -->
<KeepAlive :max="5">
    <component :is="currentTab" />
</KeepAlive>
```

#### 缓存组件的生命周期

被缓存的组件有两个额外的钩子：

```html
<script setup>
import { onActivated, onDeactivated } from 'vue'

// 组件被激活（从缓存中恢复）
onActivated(() => {
    console.log('组件被激活')
    // 可以在这里刷新数据
})

// 组件被停用（进入缓存）
onDeactivated(() => {
    console.log('组件被停用')
})
</script>
```

---

### ✏️ Task 2：Tab 切换（动态组件）（25分钟）

**目标**：练习动态组件和 KeepAlive

创建一个 Tab 切换组件：
1. 三个 Tab 页面：「商品列表」「购物车」「个人中心」
2. 使用动态组件实现切换
3. 使用 KeepAlive 保持「购物车」页面的状态

**要求**：
- 购物车页面有一个商品数量输入框
- 切换到其他 Tab 再切回来，输入的数量应该保留
- 商品列表页面不需要缓存

---

### 6.3 异步组件

对于大型组件或非首屏组件，可以使用异步加载：

```html
<script setup>
import { defineAsyncComponent } from 'vue'

// 异步加载组件
const HeavyComponent = defineAsyncComponent(() =>
    import('./HeavyComponent.vue')
)

// 带选项的异步组件
const AsyncModal = defineAsyncComponent({
    loader: () => import('./Modal.vue'),
    loadingComponent: LoadingSpinner,  // 加载中显示
    errorComponent: ErrorDisplay,      // 加载失败显示
    delay: 200,                         // 延迟显示 loading（毫秒）
    timeout: 3000                       // 超时时间
})
</script>

<template>
    <HeavyComponent />
</template>
```

---

### 6.4 Teleport 传送门

`<Teleport>` 可以将组件的 DOM 渲染到指定位置（通常用于模态框）：

```html
<template>
    <button @click="showModal = true">打开模态框</button>
    
    <!-- 将内容传送到 body 末尾 -->
    <Teleport to="body">
        <div v-if="showModal" class="modal-overlay">
            <div class="modal">
                <h2>模态框标题</h2>
                <p>模态框内容...</p>
                <button @click="showModal = false">关闭</button>
            </div>
        </div>
    </Teleport>
</template>

<script setup>
import { ref } from 'vue'
const showModal = ref(false)
</script>
```

**为什么需要 Teleport？**

模态框通常需要：
- 脱离当前组件的 DOM 层级
- 避免被父组件的 `overflow: hidden` 裁剪
- 使用固定定位覆盖整个页面

---

### ✏️ Task 3：模态框组件（插槽 + Teleport）（30分钟）

**目标**：综合运用插槽和 Teleport

创建一个可复用的 `Modal` 组件：
1. 使用 Teleport 将模态框渲染到 body
2. 使用具名插槽：header、default（内容）、footer
3. 点击遮罩层或关闭按钮可关闭模态框
4. 支持 v-model 控制显示/隐藏

**要求**：
- Modal 组件可以在任何地方使用
- 父组件可以自定义标题、内容、底部按钮
- 有动画效果（可选）

---

## 📋 综合速查表

### Props 定义

```html
<script setup>
// 简单定义
const props = defineProps(['title', 'count'])

// 带验证
const props = defineProps({
    title: { type: String, required: true },
    count: { type: Number, default: 0 }
})

// TypeScript 风格
const props = withDefaults(defineProps<{
    title: string
    count?: number
}>(), {
    count: 0
})
</script>
```

### v-model 组件

```html
<!-- 父组件 -->
<MyInput v-model="text" />
<MyInput v-model:title="title" v-model:content="content" />

<!-- 子组件 -->
<script setup>
const model = defineModel()           // 默认
const title = defineModel('title')    // 具名
</script>
```

### 插槽语法

```html
<!-- 子组件定义插槽 -->
<slot></slot>                           <!-- 默认插槽 -->
<slot name="header"></slot>             <!-- 具名插槽 -->
<slot name="item" :data="item"></slot>  <!-- 作用域插槽 -->

<!-- 父组件使用插槽 -->
<template #default>内容</template>
<template #header>标题</template>
<template #item="{ data }">{{ data }}</template>
<template #[dynamicSlotName]>动态插槽</template>  <!-- 动态插槽名 -->
```

### computed 计算属性

```html
<script setup>
import { ref, computed } from 'vue'

const count = ref(0)

// 只读计算属性
const double = computed(() => count.value * 2)

// 可写计算属性
const fullName = computed({
    get() { return firstName.value + lastName.value },
    set(val) { /* ... */ }
})
</script>
```

### watch 侦听器

```html
<script setup>
import { ref, watch, watchEffect } from 'vue'

const count = ref(0)

// 侦听单个源
watch(count, (newVal, oldVal) => { /* ... */ })

// 侦听多个源
watch([source1, source2], ([new1, new2], [old1, old2]) => { /* ... */ })

// 深度侦听
watch(obj, callback, { deep: true })

// 立即执行
watch(count, callback, { immediate: true })

// 自动追踪依赖
watchEffect(() => {
    console.log(count.value)  // 自动追踪 count
})
</script>
```

### 模板引用 ref

```html
<script setup>
import { ref, onMounted } from 'vue'

const inputRef = ref(null)
const childRef = ref(null)

onMounted(() => {
    inputRef.value.focus()           // 访问 DOM
    childRef.value.childMethod()     // 访问子组件方法
})
</script>

<template>
    <input ref="inputRef" />
    <ChildComponent ref="childRef" />
</template>
```

### 生命周期钩子

```html
<script setup>
import { onMounted, onUnmounted, onUpdated } from 'vue'

onMounted(() => { /* 挂载后 */ })
onUnmounted(() => { /* 卸载时 */ })
onUpdated(() => { /* 更新后 */ })
</script>
```

### provide / inject

```html
<!-- 祖先组件 -->
<script setup>
import { provide, ref } from 'vue'
provide('key', ref('value'))
</script>

<!-- 后代组件 -->
<script setup>
import { inject } from 'vue'
const value = inject('key', '默认值')
</script>
```

### 动态组件

```html
<component :is="currentComponent" />

<KeepAlive>
    <component :is="currentComponent" />
</KeepAlive>
```

---

## 📖 推荐资源

- [Vue 3 官方文档 - 组件深入](https://cn.vuejs.org/guide/components/registration.html)
- [Vue 3 官方文档 - 插槽](https://cn.vuejs.org/guide/components/slots.html)
- [Vue 3 官方文档 - 依赖注入](https://cn.vuejs.org/guide/components/provide-inject.html)
- [Vue 3 官方文档 - 生命周期](https://cn.vuejs.org/guide/essentials/lifecycle.html)

---

**祝学习愉快！** 🚀

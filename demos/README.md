# Vue 3 组件化进阶 - 课堂演示项目

## 📝 项目说明

这是 **Vue 3 组件化进阶** 课程的课堂演示项目，包含 7 个主题的交互式演示。

## 🎯 演示内容

### 1️⃣ Props 验证
- 基础类型验证（String, Number, Boolean）
- 必填项和默认值
- 对象/数组默认值（工厂函数）
- 自定义验证器

### 2️⃣ v-model 组件
- 传统写法（modelValue + update:modelValue）
- defineModel 新写法（Vue 3.4+）
- 多个 v-model 绑定
- v-model 修饰符

### 3️⃣ 插槽 Slots
- 默认插槽
- 具名插槽
- 作用域插槽
- 插槽后备内容
- 动态插槽名

### 4️⃣ 生命周期
- 基础生命周期流程
- 定时器场景（必须清理）
- 窗口大小监听
- DOM 操作（自动聚焦）
- 数据获取（模拟 API）

### 5️⃣ provide / inject
- 跨层级传递数据
- 响应式数据 + 修改方法
- 只读数据保护

### 6️⃣ 动态组件与 KeepAlive
- 基础动态组件切换
- KeepAlive 缓存组件状态
- 选择性缓存（include/exclude）
- onActivated / onDeactivated 钩子

### 7️⃣ Teleport
- 基础模态框
- 可复用模态框组件
- 禁用 Teleport

## 🚀 启动项目

```bash
# 安装依赖
npm install

# 启动开发服务器
npm run dev
```

访问浏览器中显示的地址（通常是 `http://localhost:5173`）

## 📂 项目结构

```
demos/
├── src/
│   ├── App.vue                      # 主应用（导航栏）
│   ├── main.js                      # 入口文件
│   ├── style.css                    # 全局样式
│   └── demos/                       # 演示组件目录
│       ├── Demo1PropsValidation.vue
│       ├── Demo2VModel.vue
│       ├── Demo3Slots.vue
│       ├── Demo4Lifecycle.vue
│       ├── Demo5ProvideInject.vue
│       ├── Demo6DynamicComponents.vue
│       ├── Demo7Teleport.vue
│       ├── props-components/        # Props 演示子组件
│       ├── vmodel-components/       # v-model 演示子组件
│       ├── slots-components/        # 插槽演示子组件
│       ├── lifecycle-components/    # 生命周期演示子组件
│       ├── provide-inject-components/ # provide/inject 演示子组件
│       ├── dynamic-components/      # 动态组件演示子组件
│       └── teleport-components/     # Teleport 演示子组件
├── index.html
├── package.json
└── vite.config.js
```

## 💡 使用建议

### 课堂演示流程

1. **启动项目**：课前启动开发服务器
2. **按顺序讲解**：点击顶部导航栏切换不同演示
3. **打开控制台**：生命周期演示需要查看控制台输出
4. **鼓励互动**：让学生修改代码、观察效果

### 重点演示技巧

#### Props 验证
- 在控制台演示类型错误警告
- 对比有无默认值的差异
- 强调对象/数组必须用工厂函数

#### v-model
- 对比传统写法和 defineModel 的代码量
- 演示多个 v-model 的实用性
- 说明 .trim 等修饰符的作用

#### 插槽
- 强调插槽的"占位"概念
- 作用域插槽是难点，多演示几次
- 展示同一个组件用不同插槽内容的效果

#### 生命周期
- **必须打开控制台**查看钩子执行顺序
- 强调清理的重要性（定时器、事件监听）
- 演示 onMounted 后 DOM 才可用

#### provide/inject
- 画图展示组件层级关系
- 对比 Props 逐层传递的繁琐
- 强调适用场景（深层嵌套）

#### 动态组件
- 先演示不缓存，让学生感受数据丢失
- 再演示 KeepAlive，体会差异
- 说明 onActivated/onDeactivated 用途

#### Teleport
- 打开开发者工具，查看 DOM 位置
- 说明模态框为什么需要 Teleport
- 演示 disabled 的作用

## 🎓 学习资源

- [Vue 3 官方文档](https://cn.vuejs.org/)
- [学生学习文档](../vue-components-advanced-student-version.md)
- [Task 练习](../task-1-card-slot/)

## 📝 注意事项

- 确保 Node.js 版本 >= 16
- 首次运行需要 `npm install` 安装依赖
- 模态框演示建议使用浏览器开发者工具查看 DOM 结构
- 生命周期演示必须打开控制台查看输出
- 所有演示都有详细的中文注释，可以展示给学生看

---

**祝教学顺利！** 🎉

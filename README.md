# Vue 3 组件化进阶 - 课程资料包

> 📚 **第 2 课** - 深入理解组件通信、插槽与生命周期

---

## 📦 资料包内容

```
course_source-20251208/
├── README.md                                    # 本文档（快速上手指南）
├── vue-components-advanced-student-version.md   # 完整学生学习文档
├── demos/                                       # 演示项目（可直接运行）
│   ├── package.json
│   ├── vite.config.js
│   ├── index.html
│   └── src/
│       ├── main.js
│       ├── App.vue
│       └── components/
├── task-1-card-slot/       # 练习1：使用插槽创建 Card 组件
├── task-2-dynamic-tabs/    # 练习2：Tab 切换（动态组件）
└── task-3-modal/           # 练习3：模态框组件（插槽 + Teleport）
```

---

## 📁 文件说明

### 📚 核心学习文档

**`vue-components-advanced-student-version.md`** - 完整学习文档（必读）

涵盖内容：
- Props 高级用法（类型验证、默认值）
- `v-model` 在组件上的使用
- 插槽（默认插槽、具名插槽、作用域插槽）
- 组件生命周期钩子
- `provide` / `inject` 跨层级传递
- 动态组件与 `<KeepAlive>`

### 🎮 演示项目

**`demos/`** - 课堂演示代码

进入目录后执行：
```bash
npm install   # 安装项目依赖
npm run dev   # 启动开发服务器
```

### ✏️ 练习题

| 目录 | 难度 | 知识点 | 预计用时 |
|------|------|--------|----------|
| `task-1-card-slot/` | 初级 | 默认插槽、具名插槽 | 20 分钟 |
| `task-2-dynamic-tabs/` | 中级 | 动态组件、KeepAlive | 25 分钟 |
| `task-3-modal/` | 进阶 | 插槽 + Teleport + 事件 | 30 分钟 |

每个练习项目包含：
- 完整的 Vite + Vue 项目结构
- 详细的任务说明（在 `App.vue` 注释中）
- 部分代码骨架（需要补全 TODO 部分）

---

## 🚀 快速开始

### 环境准备

1. **安装 Node.js**（版本 18+）  
   下载地址：https://nodejs.org/

2. **验证安装**
   ```bash
   node -v    # 应显示 v18.x.x 或更高
   npm -v     # 应显示 9.x.x 或更高
   ```

### 运行练习项目

```bash
# 以 task-1-card-slot 为例
cd task-1-card-slot
npm install
npm run dev
```

---

## 📚 学习目标

完成本课程后，你应该能够：

- [ ] 使用 Props 验证和默认值增强组件健壮性
- [ ] 在组件上使用 `v-model` 实现双向绑定
- [ ] 使用插槽创建灵活的可复用组件
- [ ] 理解组件生命周期并正确使用钩子函数
- [ ] 使用 `provide` / `inject` 解决深层组件通信
- [ ] 使用动态组件和 `<KeepAlive>` 优化用户体验

---

## ⏱️ 课程结构（150分钟）

1. **组件通信深入**（40分钟）— Props 高级、v-model、透传属性
2. **插槽 Slots**（40分钟）— 默认、具名、作用域插槽
3. **组件生命周期**（30分钟）— 钩子函数与使用场景
4. **provide / inject**（20分钟）— 跨层级数据传递
5. **动态组件与异步组件**（20分钟）— component :is、KeepAlive

---

## 🔗 相关资源

- **Vue 3 官方文档 - 组件深入**: https://cn.vuejs.org/guide/components/registration.html
- **Vue 3 官方文档 - 插槽**: https://cn.vuejs.org/guide/components/slots.html
- **Vue 3 官方文档 - 生命周期**: https://cn.vuejs.org/guide/essentials/lifecycle.html

---

## 📋 前置要求

在开始本课程前，请确保你已经掌握：

- ✅ Vite 项目创建与运行
- ✅ Vue 单文件组件（SFC）结构
- ✅ `ref` / `reactive` 响应式数据
- ✅ 常用指令（v-bind、v-on、v-if、v-for）
- ✅ 基础的 Props 传值

如果以上内容不熟悉，请先复习 **第 1 课：Vue 3 + Vite 入门**。

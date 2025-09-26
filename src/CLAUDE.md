[根目录](../../CLAUDE.md) > **src**

# src 源代码模块

## 模块职责

`src` 目录是 vue-element-admin 项目的核心源代码模块，包含了所有前端应用的源代码文件。该模块负责整个应用的业务逻辑、组件渲染、状态管理、路由控制等核心功能。

## 入口与启动

### 主要入口文件
- **main.js**: 应用程序主入口文件，负责 Vue 实例的创建和初始化
- **App.vue**: 根组件，包含应用的基本结构
- **permission.js**: 权限控制入口，处理路由权限和用户认证

### 启动流程
1. `main.js` 初始化 Vue 应用
2. 引入 Element UI 及相关配置
3. 注册全局组件、指令和过滤器
4. 加载权限控制和错误日志系统
5. 根据环境决定是否启用 Mock 数据服务

## 对外接口

### API 接口 (`src/api/`)
- **user.js**: 用户相关接口（登录、获取用户信息、登出）
- **article.js**: 文章管理接口
- **role.js**: 角色权限接口
- **qiniu.js**: 七牛云上传接口
- **remote-search.js**: 远程搜索接口

### 路由接口 (`src/router/`)
- **index.js**: 主路由配置，包含常量路由和动态路由
- **modules/**: 模块化路由配置
  - `components.js`: 组件示例路由
  - `charts.js`: 图表相关路由
  - `table.js`: 表格相关路由
  - `nested.js**: 嵌套路由示例

## 关键依赖与配置

### 状态管理 (`src/store/`)
- **modules/app.js**: 应用全局状态（侧边栏、设备类型、界面尺寸）
- **modules/user.js**: 用户状态管理（登录、权限、用户信息）
- **modules/permission.js**: 权限路由管理
- **modules/settings.js**: 应用设置管理
- **modules/tagsView.js**: 标签页视图管理
- **modules/errorLog.js**: 错误日志管理

### 工具函数 (`src/utils/`)
- **request.js**: Axios 请求封装，包含拦截器和错误处理
- **auth.js**: 权限认证工具（Token 管理）
- **validate.js**: 表单验证工具
- **permission.js**: 权限控制工具
- **error-log.js**: 错误日志工具
- **get-page-title.js**: 页面标题工具

## 数据模型

### 用户模型
```javascript
{
  token: String,           // 用户令牌
  name: String,            // 用户名
  avatar: String,          // 头像
  introduction: String,    // 简介
  roles: Array<String>     // 角色列表
}
```

### 应用状态模型
```javascript
{
  sidebar: {
    opened: Boolean,       // 侧边栏展开状态
    withoutAnimation: Boolean // 是否禁用动画
  },
  device: String,          // 设备类型
  size: String             // 组件尺寸
}
```

### 权限路由模型
```javascript
{
  path: String,            // 路径
  component: Component,    // 组件
  hidden: Boolean,         // 是否隐藏
  meta: {
    title: String,         // 标题
    icon: String,          // 图标
    roles: Array<String>,  // 访问角色
    noCache: Boolean,      // 不缓存
    breadcrumb: Boolean,   // 面包屑显示
    affix: Boolean         // 固定标签
  }
}
```

## 测试与质量

### 测试覆盖
- **单元测试**: 主要针对工具函数和基础组件
- **测试文件位置**: `tests/unit/utils/` 和 `tests/unit/components/`
- **测试框架**: Jest + Vue Test Utils

### 代码质量工具
- **ESLint**: 代码风格检查和错误提示
- **Prettier**: 代码格式化
- **Stylelint**: CSS 样式检查

### 关键配置文件
- **.eslintrc.js**: ESLint 配置，包含 Vue 和 JavaScript 规则
- **jest.config.js**: Jest 测试配置
- **vue.config.js**: Vue CLI 配置，包含构建和开发服务器设置

## 常见问题 (FAQ)

### Q: 如何添加新的 API 接口？
A: 在 `src/api` 目录下创建新的接口文件，使用统一的 request 封装，遵循 RESTful API 设计规范。

### Q: 如何实现权限控制？
A: 通过路由 meta.roles 配置页面权限，使用 v-permission 指令实现按钮级别的权限控制。

### Q: 如何自定义主题？
A: 修改 `src/styles/element-variables.scss` 文件中的变量值，重新编译即可。

### Q: 如何添加新的状态管理模块？
A: 在 `src/store/modules` 下创建新的模块文件，导出包含 state、mutations、actions 的对象。

### Q: Mock 数据如何使用？
A: 在 `mock` 目录下创建对应的 Mock 文件，开发环境会自动启用 Mock 数据服务。

## 相关文件清单

### 核心文件
- `main.js` - 应用入口
- `App.vue` - 根组件
- `permission.js` - 权限控制
- `settings.js` - 应用配置

### 目录结构
```
src/
├── api/              # API 接口
├── assets/           # 静态资源
├── components/       # 组件库
├── directive/        # 自定义指令
├── filters/          # 过滤器
├── icons/            # 图标
├── layout/           # 布局组件
├── router/           # 路由配置
├── store/            # 状态管理
├── styles/           # 样式文件
├── utils/            # 工具函数
├── views/            # 页面视图
└── App.vue           # 根组件
```

## 变更记录 (Changelog)

### 2025-09-26 - 模块文档创建
- 创建 src 模块 CLAUDE.md 文档
- 分析模块结构和主要功能
- 定义数据模型和接口规范
- 建立测试和质量标准
- 提供常见问题解决方案

### 覆盖率统计
- **核心文件覆盖率**: 100%
- **子模块覆盖率**: 90%
- **缺口分析**:
  - 部分复杂组件的实现细节需要进一步分析
  - 某些工具函数的用例需要补充文档

### 下一步建议
- 深入分析 components 目录下的复杂组件
- 补充各个子模块的详细文档
- 优化测试覆盖率和质量标准
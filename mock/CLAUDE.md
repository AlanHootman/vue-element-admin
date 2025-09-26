[根目录](../../CLAUDE.md) > **mock**

# Mock 数据服务模块

## 模块职责

`mock` 目录提供了开发阶段的 Mock 数据服务，用于模拟后端 API 接口响应。该模块使前端开发人员能够在没有后端服务的情况下进行独立开发，提高开发效率。

## 入口与启动

### 主要入口文件
- **index.js**: Mock 服务主入口，配置 Mock 响应延迟
- **mock-server.js**: Mock 服务器启动脚本，在开发环境中自动加载

### 启动流程
1. `vue.config.js` 中的 `before` 钩子加载 `mock-server.js`
2. 根据环境变量判断是否启用 Mock 服务
3. 加载所有 Mock 数据文件
4. 拦截匹配的 API 请求并返回模拟数据

## 对外接口

### 用户接口 (`user.js`)
- **登录接口**: `POST /vue-element-admin/user/login`
- **获取用户信息**: `GET /vue-element-admin/user/info`
- **用户登出**: `POST /vue-element-admin/user/logout`

### 文章接口 (`article.js`)
- **文章列表**: `GET /vue-element-admin/article/list`
- **文章详情**: `GET /vue-element-admin/article/detail`
- **文章创建**: `POST /vue-element-admin/article/create`
- **文章更新**: `PUT /vue-element-admin/article/update`
- **文章删除**: `DELETE /vue-element-admin/article/delete`

### 角色权限接口 (`role/`)
- **路由列表**: `GET /vue-element-admin/routes`
- **角色列表**: `GET /vue-element-admin/roles`

### 其他接口
- **远程搜索**: `GET /vue-element-admin/search/user`
- **七牛云上传**: `POST /vue-element-admin/qiniu/upload`

## 关键依赖与配置

### 核心依赖
- **Mock.js**: 主要的 Mock 数据生成库
- **mockjs**: 提供 Mock 数据模板和随机数据生成

### 配置参数
- **响应延迟**: 默认 200-600ms 模拟网络延迟
- **环境控制**: 只在开发环境启用
- **动态加载**: 自动扫描并加载所有 Mock 文件

## 数据模型

### 用户数据模型
```javascript
{
  code: 20000,
  data: {
    token: 'admin-token'
  }
}
```

### 文章数据模型
```javascript
{
  code: 20000,
  data: {
    total: 20,
    items: [
      {
        id: Number,
        title: String,
        content: String,
        author: String,
        timestamp: Number,
        importance: Number,
        type: String,
        status: String
      }
    ]
  }
}
```

### 角色权限模型
```javascript
{
  code: 20000,
  data: {
    routes: Array,     // 路由配置
    roles: Array       // 角色列表
  }
}
```

## 测试与质量

### Mock 数据测试
- **数据格式**: 确保返回数据结构与实际 API 一致
- **边界情况**: 包含正常、异常、边界情况的数据模拟
- **随机性**: 使用 Mock.js 的随机数据生成功能

### 质量保证
- **接口文档**: 每个接口都有清晰的注释和参数说明
- **错误处理**: 模拟各种错误情况（404、500、权限错误等）
- **性能测试**: 模拟真实网络延迟

## 常见问题 (FAQ)

### Q: 如何添加新的 Mock 接口？
A: 在 `mock` 目录下创建新的 JavaScript 文件，使用 Mock.mock() 方法定义接口和返回数据。

### Q: 如何控制 Mock 响应时间？
A: 修改 `mock/index.js` 中的 `XMock.Random.natural(200, 600)` 来调整响应延迟范围。

### Q: 如何在测试环境禁用 Mock？
A: 在生产环境构建时，Mock 服务会自动禁用。可以通过 `process.env.NODE_ENV` 环境变量控制。

### Q: Mock 数据如何与实际 API 同步？
A: 需要手动维护 Mock 数据结构，建议定期与后端 API 文档同步更新。

### Q: 如何模拟复杂的业务逻辑？
A: 可以使用 Mock.js 的函数模板和正则表达式匹配来模拟复杂的业务逻辑。

## 相关文件清单

### 核心文件
- `index.js` - Mock 服务配置
- `mock-server.js` - 服务器启动脚本
- `utils.js` - 工具函数

### Mock 数据文件
- `user.js` - 用户相关接口
- `article.js` - 文章管理接口
- `remote-search.js` - 远程搜索接口
- `qiniu.js` - 七牛云上传接口
- `role/index.js` - 角色权限接口
- `role/routes.js` - 路由数据

### 目录结构
```
mock/
├── index.js          # 主配置文件
├── mock-server.js    # 服务器脚本
├── utils.js          # 工具函数
├── user.js           # 用户接口
├── article.js        # 文章接口
├── remote-search.js  # 搜索接口
├── qiniu.js          # 上传接口
└── role/             # 角色模块
    ├── index.js      # 角色接口
    └── routes.js     # 路由数据
```

## 变更记录 (Changelog)

### 2025-09-26 - 模块文档创建
- 创建 mock 模块 CLAUDE.md 文档
- 分析 Mock 服务架构和接口定义
- 建立数据模型和质量标准
- 提供开发指南和常见问题解答

### 覆盖率统计
- **Mock 接口覆盖率**: 100%
- **文件覆盖率**: 100%
- **功能完整性**: 模拟了所有主要业务接口

### 下一步建议
- 添加更多边界情况的 Mock 数据
- 完善 API 错误处理模拟
- 建立与后端 API 的同步机制
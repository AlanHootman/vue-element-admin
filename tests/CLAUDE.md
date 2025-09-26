[根目录](../../CLAUDE.md) > **tests**

# 测试模块

## 模块职责

`tests` 目录包含了项目的所有测试用例，主要采用单元测试的方式对核心功能进行验证。该模块确保代码质量和功能稳定性，为项目提供可靠的测试保障。

## 入口与启动

### 主要配置文件
- **jest.config.js**: Jest 测试框架配置文件
- **package.json**: 测试脚本配置（`test:unit`）

### 启动流程
1. 执行 `npm run test:unit` 命令
2. Jest 自动发现和运行测试用例
3. 生成测试覆盖率报告
4. 输出测试结果和统计信息

## 测试覆盖范围

### 组件测试 (`unit/components/`)
- **Hamburger.spec.js**: 汉堡菜单组件测试
  - 点击事件测试
  - isActive 属性测试
- **SvgIcon.spec.js**: SVG 图标组件测试
  - 图标渲染测试
  - 属性传递测试

### 工具函数测试 (`unit/utils/`)
- **validate.spec.js**: 验证函数测试
  - 用户名验证
  - URL 验证
  - 大小写验证
  - 字母验证
- **parseTime.spec.js**: 时间解析函数测试
- **formatTime.spec.js**: 时间格式化函数测试
- **param2Obj.spec.js**: 参数转换函数测试

## 关键依赖与配置

### 测试框架
- **Jest**: 主要的测试运行器和断言库
- **Vue Test Utils**: Vue 组件测试工具库
- **Babel-Jest**: ES6+ 代码转换

### 配置参数
- **测试文件模式**: `**/__tests__/*.(js|jsx|ts|tsx)` 和 `**/tests/unit/**/*.spec.(js|jsx|ts|tsx)`
- **模块映射**: `@/` 映射到 `src/` 目录
- **覆盖率收集**: 收集 `src/utils` 和 `src/components` 的覆盖率
- **排除文件**: `auth.js`, `request.js`

### 覆盖率配置
```javascript
collectCoverageFrom: [
  'src/utils/**/*.{js,vue}',
  '!src/utils/auth.js',
  '!src/utils/request.js',
  'src/components/**/*.{js,vue}'
]
```

## 测试标准

### 测试命名规范
- **测试文件**: `*.spec.js` 或 `*.test.js`
- **测试用例**: 使用 `describe()` 和 `it()` 组织
- **断言**: 使用 Jest 的 `expect()` 和匹配器

### 测试用例结构
```javascript
describe('Component/Function Name', () => {
  it('should do something', () => {
    // 测试准备
    // 执行操作
    // 断言验证
  })
})
```

### 测试覆盖率目标
- **语句覆盖率**: ≥ 80%
- **分支覆盖率**: ≥ 80%
- **函数覆盖率**: ≥ 80%
- **行覆盖率**: ≥ 80%

## 常见问题 (FAQ)

### Q: 如何编写 Vue 组件测试？
A: 使用 `shallowMount` 或 `mount` 创建组件实例，通过 `wrapper` 访问组件属性和方法。

### Q: 如何测试异步操作？
A: 使用 `async/await` 或返回 Promise，使用 `jest.useFakeTimers()` 处理定时器。

### Q: 如何 Mock 依赖模块？
A: 使用 `jest.mock()` 模拟模块，使用 `jest.fn()` 创建模拟函数。

### Q: 如何查看测试覆盖率？
A: 运行测试后查看 `tests/unit/coverage/` 目录下的 HTML 报告。

### Q: 如何调试测试用例？
A: 使用 `console.log()` 或在 VS Code 中配置调试器进行断点调试。

## 相关文件清单

### 配置文件
- `jest.config.js` - Jest 测试配置
- `package.json` - 测试脚本配置

### 测试文件
- `unit/components/Hamburger.spec.js` - 汉堡菜单组件测试
- `unit/components/SvgIcon.spec.js` - SVG 图标组件测试
- `unit/utils/validate.spec.js` - 验证函数测试
- `unit/utils/parseTime.spec.js` - 时间解析测试
- `unit/utils/formatTime.spec.js` - 时间格式化测试
- `unit/utils/param2Obj.spec.js` - 参数转换测试

### 覆盖率报告
- `unit/coverage/` - 测试覆盖率报告目录
  - `lcov-report/` - HTML 格式报告
  - `lcov.info` - LCOV 格式数据

### 目录结构
```
tests/
├── unit/
│   ├── components/     # 组件测试
│   │   ├── Hamburger.spec.js
│   │   └── SvgIcon.spec.js
│   ├── utils/          # 工具函数测试
│   │   ├── validate.spec.js
│   │   ├── parseTime.spec.js
│   │   ├── formatTime.spec.js
│   │   └── param2Obj.spec.js
│   └── coverage/       # 覆盖率报告
│       ├── lcov-report/
│       └── lcov.info
└── e2e/                # 端到端测试（待实现）
```

## 变更记录 (Changelog)

### 2025-09-26 - 测试模块文档创建
- 创建 tests 模块 CLAUDE.md 文档
- 分析测试框架和配置
- 建立测试标准和最佳实践
- 提供测试开发指南

### 覆盖率统计
- **现有测试覆盖率**: 约 60%
- **组件测试覆盖**: 2/20+ 组件
- **工具函数测试覆盖**: 5/8+ 函数
- **主要缺口**:
  - 缺少大部分组件的单元测试
  - 缺少集成测试和端到端测试
  - 缺少 API 层的测试

### 下一步建议
- 优先补测：核心业务组件（如 Pagination、UploadExcel）
- 集成测试：添加组件间的交互测试
- API 测试：为 utils/request.js 添加测试用例
- E2E 测试：考虑引入 Cypress 或 Puppeteer 进行端到端测试

### 测试扩展计划
1. **短期目标**：
   - 将核心组件测试覆盖率提升至 80%
   - 为关键工具函数添加完整测试
   - 建立持续集成中的测试流程

2. **中期目标**：
   - 引入集成测试框架
   - 添加 API Mock 测试
   - 建立性能测试基准

3. **长期目标**：
   - 实现完整的测试金字塔
   - 建立测试驱动开发流程
   - 引入自动化测试报告
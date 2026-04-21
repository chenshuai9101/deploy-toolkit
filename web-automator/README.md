# web-automator - AI驱动的网页自动化工具

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Version](https://img.shields.io/badge/version-1.0.0-green.svg)
![Platform](https://img.shields.io/badge/platform-CLI%20%7C%20API-orange.svg)

> 统一网页自动化工具，融合浏览器控制、网页抓取、应用构建、自动化测试与文档生成五大能力

## 核心特性

| 功能模块 | 描述 | CLI 命令 |
|---------|------|----------|
| **浏览器自动化** | Playwright驱动的智能网页操作 | `wa do` |
| **网页抓取** | 智能内容提取与多引擎搜索 | `wa scrape` |
| **应用构建** | React/Tailwind HTML快速生成 | `wa build` |
| **自动化测试** | E2E测试与性能监控 | `wa test` |
| **文档生成** | 内部沟通与报告自动编写 | `wa docs` |

## 快速开始

### 安装

```bash
npm install -g web-automator-cli
```

### 认证

```bash
wa auth --token <your-api-token>
```

### 基础用法

```bash
# 浏览器自动化
wa do --task "登录GitHub并创建新仓库"

# 网页抓取
wa scrape --urls "https://example.com" --depth 2

# 应用构建
wa build --template "dashboard" --name "my-app"

# 自动化测试
wa test --url "https://myapp.com" --suite "e2e"

# 文档生成
wa docs --type "api-docs" --context "REST API endpoints"
```

## 统一 CLI 接口

### 命令格式

```bash
wa <action> <target> [options] --json
```

### 全局选项

| 选项 | 说明 | 默认值 |
|------|------|--------|
| `--json` | 输出JSON格式结果 | false |
| `--verbose` | 详细日志模式 | false |
| `--timeout` | 超时时间(秒) | 300 |
| `--profile` | 浏览器配置文件 | default |

## API 参考

### Node.js SDK

```javascript
import { WebAutomator } from 'web-automator-sdk';

const wa = new WebAutomator({
  apiKey: process.env.WEB_AUTOMATOR_API_KEY
});

// 浏览器自动化
const session = await wa.open('https://github.com');
await session.click('.btn-signup');
const result = await session.getResult();

// 网页抓取
const data = await wa.scrape({
  urls: ['https://news.ycombinator.com'],
  selectors: ['.titleline > a', '.score'],
  depth: 1
});

// 应用构建
const artifact = await wa.build({
  framework: 'react',
  template: 'dashboard',
  components: ['Table', 'Chart', 'Modal']
});
```

### Python SDK

```python
from web_automator import WebAutomator

wa = WebAutomator(api_key="your-api-key")

# 浏览器自动化
session = wa.open("https://github.com")
session.click(".btn-signup")
result = session.get_result()

# 网页抓取
data = wa.scrape(
    urls=["https://news.ycombinator.com"],
    selectors=[".titleline > a", ".score"],
    depth=1
)
```

## 输出格式

### JSON 结构

```json
{
  "success": true,
  "data": { ... },
  "meta": {
    "duration": 1234,
    "tokens": 567,
    "version": "1.0.0"
  },
  "errors": []
}
```

## 无状态设计

web-automator 采用无状态架构设计：

- **会话隔离**: 每个任务使用独立的浏览器上下文
- **自动清理**: 任务完成后自动释放资源
- **可扩展性**: 支持水平扩展处理并发请求

## 定价

| 套餐 | 价格 | 功能 |
|------|------|------|
| Free | $0 | 本地浏览器 + 100次/月 |
| Pro | $12.99/mo | 云端 + 无限爬虫 + 并行任务 |
| Enterprise | 定制 | 分布式 + 私有部署 + SLA |

## 文档

- [使用示例](./examples/)
- [模板库](./templates/)
- [API 文档](https://docs.web-automator.dev)

## 许可证

MIT License - 详见 [LICENSE](./LICENSE) 文件

## 贡献

欢迎提交 Issue 和 Pull Request！

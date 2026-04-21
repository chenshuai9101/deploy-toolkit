# web-automator SKILL

> AI Agent 网页自动化工具 | Playwright驱动 | 无状态设计

## 概述

web-automator 是为 AI Agent 设计的网页自动化 Skill，统一了以下五大能力：

| 原Skill | 能力来源 | 功能 |
|---------|---------|------|
| agent-browser | Playwright | 云端浏览器代理与控制 |
| firecrawl | 智能爬虫 | 网页内容抓取与搜索 |
| artifacts-builder | React/Tailwind | Web产物快速构建 |
| webapp-testing | Playwright | E2E自动化测试 |
| internal-comms | 文档引擎 | 内部沟通文档生成 |

## CLI 命令格式

```bash
wa <action> <target> [options]
```

### 命令列表

| 命令 | 说明 | 选项 |
|------|------|------|
| `wa do` | 执行自动化任务 | `--task`, `--url`, `--profile` |
| `wa scrape` | 网页内容抓取 | `--urls`, `--selectors`, `--depth` |
| `wa build` | 应用构建 | `--template`, `--framework`, `--name` |
| `wa test` | 自动化测试 | `--url`, `--suite`, `--report` |
| `wa docs` | 文档生成 | `--type`, `--context`, `--format` |

## 统一接口

### 1. 浏览器自动化 (Browser Automation)

```bash
# 基本用法
wa do --task "登录GitHub并创建仓库"

# 高级用法
wa do \
  --task "填写表单并提交" \
  --url "https://form.example.com" \
  --fields '{"username": "test", "email": "test@example.com"}' \
  --profile "headless" \
  --json
```

**JSON 输出示例:**
```json
{
  "success": true,
  "command": "do",
  "data": {
    "sessionId": "sess_abc123",
    "actions": [
      {"type": "navigate", "url": "https://github.com/login"},
      {"type": "fill", "selector": "#login_field", "value": "user"},
      {"type": "click", "selector": ".btn-signup"}
    ],
    "screenshots": ["/tmp/screenshot_1.png"],
    "result": "Form submitted successfully"
  },
  "meta": {
    "duration": 4523,
    "steps": 5,
    "browser": "chromium"
  }
}
```

### 2. 网页抓取 (Web Scraping)

```bash
# 单页抓取
wa scrape --urls "https://news.ycombinator.com"

# 多页深度抓取
wa scrape \
  --urls "https://example.com,https://example.com/page2" \
  --selectors ".title,.content,.author" \
  --depth 2 \
  --format "markdown" \
  --json
```

**JSON 输出示例:**
```json
{
  "success": true,
  "command": "scrape",
  "data": {
    "pages": [
      {
        "url": "https://news.ycombinator.com",
        "content": [
          {"selector": ".title", "text": "Example News Title"},
          {"selector": ".content", "text": "News content..."}
        ],
        "metadata": {
          "title": "Hacker News",
          "links": 30,
          "images": 5
        }
      }
    ],
    "exported": "/tmp/scrape_results.json"
  },
  "meta": {
    "duration": 1234,
    "pages": 1,
    "items": 45
  }
}
```

### 3. 应用构建 (App Building)

```bash
# 使用模板构建
wa build --template "dashboard" --name "my-dashboard"

# 自定义构建
wa build \
  --framework "react" \
  --template "dashboard" \
  --name "analytics-app" \
  --components "Table,Chart,Modal,Form" \
  --styling "tailwind" \
  --json
```

**JSON 输出示例:**
```json
{
  "success": true,
  "command": "build",
  "data": {
    "projectId": "proj_xyz789",
    "framework": "react",
    "template": "dashboard",
    "files": [
      {"path": "src/App.tsx", "lines": 120},
      {"path": "src/components/Table.tsx", "lines": 85},
      {"path": "src/components/Chart.tsx", "lines": 92}
    ],
    "preview": "https://preview.web-automator.dev/xyz789",
    "installCommand": "npm install && npm run dev"
  },
  "meta": {
    "duration": 8923,
    "components": 3,
    "dependencies": 24
  }
}
```

### 4. 自动化测试 (Testing)

```bash
# 运行E2E测试
wa test --url "https://myapp.com" --suite "e2e"

# 性能测试
wa test \
  --url "https://myapp.com" \
  --suite "performance" \
  --report "html" \
  --json
```

**JSON 输出示例:**
```json
{
  "success": true,
  "command": "test",
  "data": {
    "suite": "e2e",
    "results": {
      "total": 25,
      "passed": 23,
      "failed": 2,
      "skipped": 0
    },
    "tests": [
      {
        "name": "Login Flow",
        "status": "passed",
        "duration": 1234,
        "screenshots": ["/reports/login.png"]
      },
      {
        "name": "Payment Process",
        "status": "failed",
        "error": "Timeout waiting for element #pay-btn"
      }
    ],
    "report": "/reports/test-report.html"
  },
  "meta": {
    "duration": 45234,
    "browser": "chromium",
    "viewport": "1920x1080"
  }
}
```

### 5. 文档生成 (Documentation)

```bash
# API文档
wa docs --type "api-docs" --context "REST endpoints"

# 测试报告
wa docs \
  --type "test-report" \
  --context "E2E test results" \
  --format "markdown" \
  --json
```

**JSON 输出示例:**
```json
{
  "success": true,
  "command": "docs",
  "data": {
    "type": "api-docs",
    "content": "# API Documentation\n\n## Endpoints\n\n### GET /users\n\nRetrieves a list of users...",
    "format": "markdown",
    "exported": "/tmp/api-docs.md"
  },
  "meta": {
    "duration": 2341,
    "tokens": 1523,
    "format": "markdown"
  }
}
```

## Agent 集成指南

### 工具调用模式

```javascript
// Agent 调用 web-automator
const result = await agent.callTool('web-automator', {
  action: 'do',
  task: '登录并发布文章',
  params: {
    url: 'https://medium.com/write',
    credentials: {
      username: '${USER_NAME}',
      password: '${USER_PASSWORD}'
    },
    output: 'json'
  }
});
```

### 错误处理

```json
{
  "success": false,
  "error": {
    "code": "ELEMENT_NOT_FOUND",
    "message": "Selector '#submit-btn' not found within 30s",
    "suggestion": "Check if the page loaded correctly or try alternative selector"
  },
  "meta": {
    "duration": 30234,
    "attempt": 1
  }
}
```

### 错误码

| 错误码 | 说明 | 处理建议 |
|--------|------|----------|
| `ELEMENT_NOT_FOUND` | 元素未找到 | 增加等待时间或更换选择器 |
| `TIMEOUT` | 操作超时 | 增加 timeout 参数 |
| `AUTH_FAILED` | 认证失败 | 检查凭证是否正确 |
| `RATE_LIMITED` | 请求过于频繁 | 添加延迟或使用代理 |
| `PAGE_CRASH` | 页面崩溃 | 刷新页面或重启会话 |

## 配置项

### 全局配置

```json
{
  "web-automator": {
    "defaultProfile": "default",
    "timeout": 30000,
    "headless": true,
    "viewport": {
      "width": 1920,
      "height": 1080
    },
    "userAgent": "WebAutomator/1.0",
    "proxy": null
  }
}
```

### 浏览器配置

```json
{
  "profiles": {
    "default": {
      "browser": "chromium",
      "headless": false
    },
    "stealth": {
      "browser": "chromium",
      "headless": true,
      "userAgent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36"
    }
  }
}
```

## 无状态设计原则

1. **会话隔离**: 每次任务使用独立的浏览器上下文
2. **自动清理**: 任务完成后自动关闭浏览器、清理 cookies
3. **幂等操作**: 相同输入产生相同输出
4. **可恢复性**: 支持从检查点恢复执行

## 技术栈

- **浏览器引擎**: Playwright (Chromium, Firefox, WebKit)
- **Node.js SDK**: TypeScript + Node.js 18+
- **Python SDK**: Python 3.11+
- **API**: RESTful JSON API

## 限制与配额

| 套餐 | 每日请求 | 并发 | 存储 |
|------|----------|------|------|
| Free | 100 | 1 | 100MB |
| Pro | 10,000 | 10 | 10GB |
| Enterprise | 无限制 | 自定义 | 无限制 |

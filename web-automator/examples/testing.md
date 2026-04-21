# web-automator 测试示例

## 1. E2E 测试

### 登录流程测试

```bash
# 测试用户登录
wa test \
  --url "https://app.example.com" \
  --suite "login" \
  --test-cases '[
    {
      "name": "valid-login",
      "steps": [
        {"action": "navigate", "url": "/login"},
        {"action": "fill", "selector": "#email", "value": "user@example.com"},
        {"action": "fill", "selector": "#password", "value": "password123"},
        {"action": "click", "selector": "button[type=submit]"},
        {"action": "wait-for", "selector": ".dashboard"},
        {"action": "assert", "condition": "url.includes(dashboard)"}
      ]
    },
    {
      "name": "invalid-login",
      "steps": [
        {"action": "navigate", "url": "/login"},
        {"action": "fill", "selector": "#email", "value": "invalid@email.com"},
        {"action": "fill", "selector": "#password", "value": "wrongpass"},
        {"action": "click", "selector": "button[type=submit]"},
        {"action": "assert", "condition": "selector-visible(.error-message)"}
      ]
    }
  ]' \
  --json
```

### 购物车测试

```bash
# 测试完整购物流程
wa test \
  --url "https://shop.example.com" \
  --suite "checkout" \
  --test-cases '[
    {
      "name": "add-to-cart",
      "steps": [
        {"action": "click", "selector": ".product:first-child"},
        {"action": "click", "selector": ".btn-add-cart"},
        {"action": "assert", "condition": "selector-text(.cart-count, 1)"}
      ]
    },
    {
      "name": "checkout-flow",
      "steps": [
        {"action": "click", "selector": ".btn-checkout"},
        {"action": "fill", "selector": "#shipping-name", "value": "John Doe"},
        {"action": "fill", "selector": "#shipping-address", "value": "123 Main St"},
        {"action": "click", "selector": ".btn-continue"},
        {"action": "click", "selector": ".btn-place-order"},
        {"action": "assert", "condition": "selector-visible(.order-confirmation)"}
      ]
    }
  ]' \
  --json
```

## 2. 视觉回归测试

### 截图对比

```bash
# 视觉回归测试
wa test \
  --url "https://app.example.com/dashboard" \
  --suite "visual" \
  --visual-regression {
    "baseline": "./screenshots/baseline",
    "latest": "./screenshots/latest",
    "diff": "./screenshots/diff",
    "threshold": 0.1
  } \
  --browsers ["chromium", "firefox", "webkit"] \
  --viewports ["1920x1080", "1366x768", "375x667"] \
  --json
```

### 组件测试

```bash
# 组件视觉测试
wa test \
  --url "https://storybook.example.com" \
  --suite "components" \
  --components ["Button", "Input", "Modal", "Dropdown"] \
  --visual-regression true \
  --json
```

## 3. 性能测试

### 页面性能

```bash
# 性能基准测试
wa test \
  --url "https://app.example.com" \
  --suite "performance" \
  --metrics ["FCP", "LCP", "CLS", "TTFB", "TBT"] \
  --thresholds {
    "FCP": 2000,
    "LCP": 4000,
    "CLS": 0.1,
    "TTFB": 800,
    "TBT": 300
  } \
  --json
```

### 负载测试

```bash
# 并发负载测试
wa test \
  --url "https://api.example.com/users" \
  --suite "load" \
  --load-test {
    "concurrent": 50,
    "duration": "60s",
    "rampUp": "10s"
  } \
  --json
```

## 4. 跨浏览器测试

### 多浏览器兼容性

```bash
# 跨浏览器测试
wa test \
  --url "https://app.example.com" \
  --suite "cross-browser" \
  --browsers ["chromium", "firefox", "webkit", "edge"] \
  --test-cases '[{"name": "basic-render", "assert": "selector-visible(.app)"}]' \
  --json
```

### 响应式测试

```bash
# 响应式布局测试
wa test \
  --url "https://app.example.com" \
  --suite "responsive" \
  --viewports [
    {"name": "mobile", "width": 375, "height": 667},
    {"name": "tablet", "width": 768, "height": 1024},
    {"name": "desktop", "width": 1920, "height": 1080},
    {"name": "4k", "width": 3840, "height": 2160}
  ] \
  --test-cases '[{"name": "layout-breaks", "assert": "no-overflow"}]' \
  --json
```

## 5. API 测试

### REST API 测试

```bash
# API 端点测试
wa test \
  --url "https://api.example.com" \
  --suite "api" \
  --api-tests '[
    {
      "name": "get-users",
      "method": "GET",
      "path": "/users",
      "assert": {"status": 200, "body.users": "array"}
    },
    {
      "name": "create-user",
      "method": "POST",
      "path": "/users",
      "body": {"name": "Test User", "email": "test@example.com"},
      "assert": {"status": 201, "body.id": "not-null"}
    }
  ]' \
  --json
```

### GraphQL 测试

```bash
# GraphQL 测试
wa test \
  --url "https://api.example.com/graphql" \
  --suite "graphql" \
  --graphql {
    "endpoint": "/graphql",
    "queries": [
      {
        "name": "getUser",
        "query": "query { user(id: 1) { id name email } }",
        "assert": {"data.user.name": "exists"}
      }
    ]
  } \
  --json
```

## 6. 报告生成

### HTML 报告

```bash
# 生成HTML报告
wa test \
  --url "https://app.example.com" \
  --suite "full" \
  --report {
    "format": "html",
    "output": "./reports/test-results.html",
    "includeScreenshots": true,
    "includeVideos": true
  } \
  --json
```

### CI/CD 集成

```bash
# JUnit XML 输出
wa test \
  --url "https://app.example.com" \
  --suite "e2e" \
  --report {
    "format": "junit",
    "output": "./reports/TEST-results.xml"
  } \
  --ci true \
  --fail-fast true \
  --json
```

### Slack 通知

```bash
# 测试完成发送通知
wa test \
  --url "https://app.example.com" \
  --suite "e2e" \
  --notify {
    "slack": {
      "webhook": "${SLACK_WEBHOOK}",
      "on": ["failure", "success"],
      "channel": "#test-results"
    }
  } \
  --json
```

## 7. 调试模式

### 逐步执行

```bash
# 调试模式
wa test \
  --url "https://app.example.com" \
  --suite "debug" \
  --test-cases '[{"name": "login", "steps": [...]}]' \
  --debug {
    "stepDelay": 1000,
    "screenshotEachStep": true,
    "consoleOutput": true,
    "networkLog": true
  } \
  --json
```

### 录制视频

```bash
# 录制测试视频
wa test \
  --url "https://app.example.com" \
  --suite "e2e" \
  --record {
    "video": true,
    "output": "./videos/test-run.mp4",
    "fps": 30
  } \
  --json
```

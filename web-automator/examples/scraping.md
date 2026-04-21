# web-automator 抓取示例

## 1. 基础抓取

### 单页面抓取

```bash
# 抓取新闻标题
wa scrape \
  --urls "https://news.ycombinator.com" \
  --selectors ".titleline > a,.score" \
  --json
```

**输出:**
```json
{
  "success": true,
  "data": {
    "pages": [{
      "url": "https://news.ycombinator.com",
      "items": [
        {"title": "Show HN: I built...", "score": "245 points"},
        {"title": "Ask HN: What...", "score": "89 points"}
      ]
    }]
  }
}
```

## 2. 深度抓取

### 整站抓取

```bash
# 抓取整个博客
wa scrape \
  --urls "https://blog.example.com" \
  --selectors "article h2,article .content,.post-meta" \
  --depth 3 \
  --follow-links true \
  --exclude "/tag/,/author/,/page/" \
  --json
```

### 分页抓取

```bash
# 抓取多页商品列表
wa scrape \
  --urls "https://shop.example.com/category/electronics?page=1" \
  --selectors ".product-name,.product-price,.product-rating" \
  --pagination {
    "selector": ".next-page",
    "maxPages": 10
  } \
  --json
```

## 3. 智能抓取

### AI 智能提取

```bash
# 使用AI理解页面结构
wa scrape \
  --urls "https://medium.com/article/how-to-code" \
  --ai-extract true \
  --ai-prompt "提取文章标题、作者、主要观点和代码示例" \
  --json
```

### 结构化数据提取

```bash
# 提取JSON-LD数据
wa scrape \
  --urls "https://recipe.example.com/pasta" \
  --extract-type "json-ld" \
  --schema "Recipe" \
  --json
```

## 4. 登录后抓取

### 认证抓取

```bash
# 登录后抓取
wa scrape \
  --urls "https://dashboard.example.com/reports" \
  --auth {
    "type": "form",
    "loginUrl": "https://example.com/login",
    "username": "user@example.com",
    "password": "password123"
  } \
  --selectors ".report-title,.report-data" \
  --json
```

### Cookie 认证

```bash
# 使用Cookie抓取
wa scrape \
  --urls "https://example.com/private-page" \
  --cookies "./auth/cookies.json" \
  --selectors ".private-content" \
  --json
```

## 5. 批量抓取

### 站点地图抓取

```bash
# 从sitemap抓取
wa scrape \
  --mode "sitemap" \
  --sitemap-url "https://example.com/sitemap.xml" \
  --selectors "article,.product-item" \
  --depth 2 \
  --json
```

### CSV 批量导入

```bash
# 从CSV读取URL列表
wa scrape \
  --input "./urls.csv" \
  --url-column "url" \
  --selectors ".title,.description,.price" \
  --output "./results.json" \
  --json
```

## 6. 高级选项

### 自定义请求头

```bash
# 自定义请求头
wa scrape \
  --urls "https://api.example.com/data" \
  --headers '{
    "Authorization": "Bearer token123",
    "Accept-Language": "en-US"
  }' \
  --json
```

### 代理轮换

```bash
# 使用代理池
wa scrape \
  --urls "https://example.com/page1,https://example.com/page2" \
  --proxy "./proxies.txt" \
  --proxy-rotate "round-robin" \
  --selectors ".content" \
  --json
```

### 速率限制

```bash
# 控制请求速率
wa scrape \
  --urls "https://site.example.com/items" \
  --rate-limit {
    "requests": 1,
    "perSeconds": 2
  } \
  --selectors ".item" \
  --json
```

## 7. 数据导出

### 多格式导出

```bash
# 导出为多种格式
wa scrape \
  --urls "https://blog.example.com" \
  --selectors "article" \
  --export {
    "json": "./results.json",
    "csv": "./results.csv",
    "markdown": "./results.md"
  } \
  --json
```

### 数据库导出

```bash
# 导出到数据库
wa scrape \
  --urls "https://products.example.com" \
  --selectors ".product" \
  --export {
    "type": "postgresql",
    "table": "products",
    "connection": "postgres://user:pass@host/db"
  } \
  --json
```

## 8. 错误处理

### 重试机制

```bash
# 失败自动重试
wa scrape \
  --urls "https://unreliable.example.com" \
  --selectors ".content" \
  --retry {
    "maxAttempts": 3,
    "delaySeconds": 5,
    "backoff": "exponential"
  } \
  --json
```

### 死链跳过

```bash
# 跳过无法访问的页面
wa scrape \
  --urls "https://example.com/pages" \
  --selectors ".content" \
  --on-error "skip" \
  --continue-on-error true \
  --json
```

# web-automator 自动化示例

## 1. 社交媒体自动化

### 自动化发帖

```bash
# LinkedIn 发帖
wa do \
  --task "登录LinkedIn并发布动态" \
  --url "https://linkedin.com" \
  --credentials '{"email":"user@email.com","password":"pass"}' \
  --action "post" \
  --content "使用 web-automator 自动化工作流程，提升10倍效率！" \
  --json
```

### Twitter 互动

```bash
# 自动点赞和转发
wa do \
  --task "搜索#AI话题并点赞前5条" \
  --url "https://twitter.com/search?q=%23AI" \
  --action "like-top-5" \
  --json
```

## 2. 数据采集

### 新闻聚合

```bash
# 采集多个新闻源
wa scrape \
  --urls "https://news.ycombinator.com,https://techcrunch.com,https://theverge.com" \
  --selectors ".titleline a,.post-title,.article-title" \
  --depth 1 \
  --format "json" \
  --json
```

### 电商价格监控

```bash
# 监控商品价格
wa scrape \
  --urls "https://amazon.com/product/B09V3KXJPB" \
  --selectors ".price-to-pay, .product-title" \
  --schedule "daily" \
  --json
```

## 3. 表单处理

### 批量注册

```bash
# 自动化用户注册
wa do \
  --task "填写注册表单" \
  --url "https://example.com/register" \
  --fields '{
    "firstName": "John",
    "lastName": "Doe",
    "email": "john.doe@example.com",
    "password": "SecurePass123!",
    "country": "United States"
  }' \
  --submit ".btn-register" \
  --json
```

### 问卷调查

```bash
# 自动填写问卷
wa do \
  --task "完成问卷调查" \
  --url "https://survey.example.com" \
  --answers '{
    "q1": "Very Satisfied",
    "q2": "Monthly",
    "q3": ["Option A", "Option C"],
    "q4": 5
  }' \
  --json
```

## 4. 截图与文档

### 批量截图

```bash
# 批量网页截图
wa do \
  --task "截图整个页面" \
  --urls "https://example.com/page1,https://example.com/page2" \
  --screenshot "fullpage" \
  --output "./screenshots/" \
  --json
```

### PDF 导出

```bash
# 导出页面为PDF
wa do \
  --task "导出为PDF" \
  --url "https://docs.example.com/report" \
  --output "./reports/report.pdf" \
  --format "pdf" \
  --json
```

## 5. 登录流程

### GitHub 自动化

```bash
# GitHub 登录并创建仓库
wa do \
  --task "登录GitHub并创建新仓库" \
  --url "https://github.com/new" \
  --credentials '{
    "username": "myusername",
    "password": "mypassword"
  }' \
  --repo-name "web-automator-test" \
  --description "Testing web-automator automation" \
  --json
```

## 6. 文件上传

### 云存储上传

```bash
# 上传文件到云存储
wa do \
  --task "上传文件到Google Drive" \
  --url "https://drive.google.com" \
  --action "upload" \
  --file "./data/report.csv" \
  --folder "web-automator Results" \
  --json
```

## 7. 复杂工作流

### 多步骤表单

```bash
# 多步骤向导表单
wa do \
  --task "完成3步注册流程" \
  --url "https://app.example.com/signup" \
  --workflow '{
    "step1": {
      "url": "https://app.example.com/signup/step1",
      "fields": {"email": "test@example.com"}
    },
    "step2": {
      "url": "https://app.example.com/signup/step2",
      "fields": {"name": "Test User"}
    },
    "step3": {
      "url": "https://app.example.com/signup/step3",
      "action": "submit"
    }
  }' \
  --json
```

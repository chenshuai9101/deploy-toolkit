# web-automator 模板库

## 1. 仪表盘模板

### React 仪表盘

```bash
wa build \
  --framework "react" \
  --template "dashboard" \
  --name "my-dashboard" \
  --components "Sidebar,Header,StatsCards,DataTable,Chart,Modal" \
  --json
```

**生成文件结构:**
```
my-dashboard/
├── src/
│   ├── App.tsx
│   ├── components/
│   │   ├── Sidebar.tsx
│   │   ├── Header.tsx
│   │   ├── StatsCards.tsx
│   │   ├── DataTable.tsx
│   │   ├── Chart.tsx
│   │   └── Modal.tsx
│   └── styles/
│       └── index.css
├── package.json
└── README.md
```

## 2. 表单模板

### 多步表单

```bash
wa build \
  --framework "react" \
  --template "multi-step-form" \
  --name "lead-capture" \
  --fields "name,email,phone,company,message" \
  --steps 3 \
  --validation "email,phone" \
  --json
```

## 3. 电商模板

### 产品列表页

```bash
wa build \
  --framework "react" \
  --template "product-list" \
  --name "store-front" \
  --features "search,filter,sort,pagination,cart" \
  --json
```

## 4. 登录/注册模板

### 认证页面

```bash
wa build \
  --framework "react" \
  --template "auth" \
  --name "auth-pages" \
  --features "login,register,forgot-password,social-login" \
  --json
```

## 5. 博客模板

### 博客系统

```bash
wa build \
  --framework "react" \
  --template "blog" \
  --name "my-blog" \
  --features "posts,comments,categories,tags,search" \
  --json
```

## 6. 管理后台模板

### Admin Panel

```bash
wa build \
  --framework "react" \
  --template "admin" \
  --name "admin-panel" \
  --modules "users,products,orders,analytics,settings" \
  --json
```

## 7. Landing Page 模板

### 营销页面

```bash
wa build \
  --framework "react" \
  --template "landing" \
  --name "product-landing" \
  --sections "hero,features,pricing,testimonials,cta,footer" \
  --json
```

## 8. API 文档模板

### Swagger/OpenAPI

```bash
wa build \
  --template "api-docs" \
  --name "api-documentation" \
  --format "openapi" \
  --json
```

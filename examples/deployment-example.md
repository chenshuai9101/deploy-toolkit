# 部署示例

## 示例 1: 部署 Node.js 应用到 AWS

```bash
# 1. 认证配置
deploy auth --provider aws --access-key AKIAIOSFODNN7EXAMPLE --secret-key wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY

# 2. 创建应用
deploy app create --name nodejs-app --type nodejs

# 3. 部署应用
deploy app deploy \
  --name nodejs-app \
  --platform aws \
  --target production \
  --instance-type t3.medium \
  --region us-east-1 \
  --auto-scaling \
  --min-instances 2 \
  --max-instances 10

# 4. 查看部署状态
deploy app status --name nodejs-app --verbose

# 5. 获取访问地址
deploy app endpoint --name nodejs-app
```

## 示例 2: 使用 Docker Compose 部署

```bash
# 1. 创建 docker-compose.yml
cat > docker-compose.yml << 'YAML'
version: '3.8'
services:
  web:
    image: nginx:alpine
    ports:
      - "80:80"
  api:
    image: my-api:latest
    environment:
      - DATABASE_URL=postgres://db:5432/myapp
    depends_on:
      - db
  db:
    image: postgres:14
    volumes:
      - db-data:/var/lib/postgresql/data
volumes:
  db-data:
YAML

# 2. 启动服务
deploy container up --file docker-compose.yml

# 3. 扩缩容
deploy container scale --service api --replicas 5

# 4. 查看日志
deploy container logs --service api --tail 100
```

## 示例 3: 设置 CI/CD 流水线

```bash
# 1. 创建流水线
deploy pipeline create \
  --name my-ci-cd \
  --repo https://github.com/user/my-app \
  --template nodejs \
  --branches main,develop

# 2. 配置环境变量
deploy pipeline env --name my-ci-cd \
  --set DATABASE_URL=postgres://prod:5432/app \
  --set API_KEY=xxx

# 3. 触发构建
deploy pipeline run --name my-ci-cd --branch main

# 4. 查看构建状态
deploy pipeline status --name my-ci-cd --run-id run_123
```

## 示例 4: 配置监控告警

```bash
# 1. 启用监控
deploy monitor enable --service my-app

# 2. 设置告警规则
deploy monitor alert \
  --service my-app \
  --rule cpu-usage \
  --threshold 80 \
  --action email \
  --recipients admin@example.com

deploy monitor alert \
  --service my-app \
  --rule error-rate \
  --threshold 1 \
  --action slack \
  --webhook https://hooks.slack.com/services/xxx

# 3. 查看监控仪表板
deploy monitor dashboard --service my-app
```

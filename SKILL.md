# deploy-toolkit SKILL
> AI Agent 部署工具包 | 多平台支持 | 统一 CLI

## 概述

deploy-toolkit 是为 AI Agent 设计的部署自动化 Skill，统一了以下五大能力：

| 原Skill | 能力来源 | 功能 |
|---------|---------|------|
| aws-deploy | AWS SDK | AWS 云资源部署 |
| docker-compose | Compose | 容器编排管理 |
| ci-cd-builder | GitHub Actions | 流水线构建 |
| monitoring-tool | CloudWatch | 监控告警系统 |
| config-manager | Config | 配置版本管理 |

## CLI 命令格式

```bash
deploy <resource> <action> [options]
```

### 命令列表

| 命令 | 说明 | 选项 |
|------|------|------|
| `deploy app deploy` | 部署应用 | `--name`, `--platform`, `--target` |
| `deploy app status` | 查看状态 | `--name`, `--verbose` |
| `deploy app rollback` | 版本回滚 | `--name`, `--version` |
| `deploy container up` | 启动容器 | `--file`, `--scale` |
| `deploy container scale` | 扩缩容 | `--service`, `--replicas` |
| `deploy pipeline create` | 创建流水线 | `--name`, `--repo` |
| `deploy pipeline run` | 运行流水线 | `--name`, `--branch` |
| `deploy monitor status` | 监控状态 | `--service` |
| `deploy monitor alert` | 设置告警 | `--rule`, `--threshold` |
| `deploy config sync` | 配置同步 | `--env`, `--target` |

## 统一接口

### 1. 应用部署 (App Deployment)

```bash
# 基本部署
deploy app deploy --name my-app --platform aws --target production

# 自定义配置
deploy app deploy \
  --name my-app \
  --platform aws \
  --target production \
  --instance-type t3.medium \
  --region us-east-1 \
  --auto-scaling \
  --json
```

**JSON 输出示例:**

```json
{
  "success": true,
  "command": "app.deploy",
  "data": {
    "app_id": "app_abc123",
    "name": "my-app",
    "platform": "aws",
    "target": "production",
    "status": "deploying",
    "resources": {
      "instance_type": "t3.medium",
      "region": "us-east-1",
      "auto_scaling": true
    },
    "endpoint": null
  },
  "meta": {
    "duration": 0,
    "cost": 0.0,
    "version": "1.0.0"
  }
}
```

### 2. 容器编排 (Container Orchestration)

```bash
# 启动服务
deploy container up --file docker-compose.yml

# 扩缩容
deploy container scale --service api --replicas 5 --json
```

**JSON 输出示例:**

```json
{
  "success": true,
  "command": "container.scale",
  "data": {
    "service": "api",
    "current_replicas": 3,
    "target_replicas": 5,
    "status": "scaling"
  },
  "meta": {
    "duration": 2341,
    "containers": 15,
    "version": "1.0.0"
  }
}
```

### 3. CI/CD 流水线 (Pipeline)

```bash
# 创建流水线
deploy pipeline create \
  --name ci-cd \
  --repo https://github.com/user/repo \
  --template nodejs \
  --json

# 触发构建
deploy pipeline run --name ci-cd --branch main --json
```

**JSON 输出示例:**

```json
{
  "success": true,
  "command": "pipeline.run",
  "data": {
    "pipeline_id": "pipe_xyz789",
    "name": "ci-cd",
    "run_id": "run_123",
    "status": "running",
    "stages": [
      {"name": "build", "status": "passed"},
      {"name": "test", "status": "running"},
      {"name": "deploy", "status": "pending"}
    ]
  },
  "meta": {
    "duration": 0,
    "version": "1.0.0"
  }
}
```

### 4. 监控告警 (Monitoring)

```bash
# 查看服务状态
deploy monitor status --service my-app --json

# 设置 CPU 告警
deploy monitor alert \
  --service my-app \
  --rule cpu-usage \
  --threshold 80 \
  --action notify \
  --json
```

**JSON 输出示例:**

```json
{
  "success": true,
  "command": "monitor.status",
  "data": {
    "service": "my-app",
    "metrics": {
      "cpu_usage": 45.2,
      "memory_usage": 62.8,
      "request_rate": 1234,
      "error_rate": 0.01
    },
    "health": "healthy",
    "uptime": 99.95
  },
  "meta": {
    "duration": 1234,
    "period": "5m",
    "version": "1.0.0"
  }
}
```

### 5. 配置管理 (Config Management)

```bash
# 同步配置
deploy config sync --env production --target all --json
```

**JSON 输出示例:**

```json
{
  "success": true,
  "command": "config.sync",
  "data": {
    "env": "production",
    "synced": [
      {"key": "DATABASE_URL", "status": "synced"},
      {"key": "API_KEY", "status": "synced"},
      {"key": "LOG_LEVEL", "status": "synced"}
    ],
    "failed": []
  },
  "meta": {
    "duration": 892,
    "total": 3,
    "version": "1.0.0"
  }
}
```

## Agent 集成指南

### 工具调用模式

```javascript
// Agent 调用 deploy-toolkit
const result = await agent.callTool('deploy-toolkit', {
  resource: 'app',
  action: 'deploy',
  params: {
    name: 'my-service',
    platform: 'aws',
    target: 'production',
    config: {
      instance_type: 't3.medium',
      region: 'us-east-1',
      auto_scaling: true
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
    "code": "DEPLOYMENT_FAILED",
    "message": "Deployment failed due to resource limit",
    "suggestion": "Try reducing instance count or using a different region"
  },
  "meta": {
    "duration": 45234,
    "attempt": 1
  }
}
```

### 错误码

| 错误码 | 说明 | 处理建议 |
|--------|------|----------|
| `AUTH_FAILED` | 认证失败 | 检查 API 密钥配置 |
| `RESOURCE_LIMIT` | 资源超限 | 降低配置或更换区域 |
| `DEPLOYMENT_FAILED` | 部署失败 | 检查日志或回滚 |
| `TIMEOUT` | 操作超时 | 增加超时时间 |
| `INVALID_CONFIG` | 配置无效 | 检查配置文件格式 |

## 配置项

### 全局配置

```json
{
  "deploy-toolkit": {
    "default_platform": "aws",
    "default_target": "production",
    "timeout": 300000,
    "retry_count": 3,
    "output_format": "json"
  }
}
```

### 平台配置

```json
{
  "platforms": {
    "aws": {
      "region": "us-east-1",
      "access_key_id": "${AWS_ACCESS_KEY_ID}",
      "secret_access_key": "${AWS_SECRET_ACCESS_KEY}"
    },
    "gcp": {
      "project_id": "my-project",
      "service_account": "${GCP_SERVICE_ACCOUNT}"
    },
    "azure": {
      "subscription_id": "${AZURE_SUBSCRIPTION_ID}",
      "tenant_id": "${AZURE_TENANT_ID}"
    }
  }
}
```

## 无状态设计原则

1. **幂等操作**: 相同配置产生相同结果
2. **状态外化**: 部署状态存储在外部系统
3. **可恢复性**: 支持从失败点恢复
4. **可追溯性**: 完整记录每次操作

## 技术栈

- **Node.js SDK**: TypeScript + Node.js 18+
- **Python SDK**: Python 3.11+
- **云 SDK**: AWS SDK, GCP SDK, Azure SDK
- **容器**: Docker API, Kubernetes Client
- **API**: RESTful JSON API

## 限制与配额

| 套餐 | 每日部署 | 并发 | 平台 |
|------|----------|------|------|
| Free | 10 | 1 | 1 |
| Pro | 1000 | 10 | 全平台 |
| Enterprise | 无限制 | 自定义 | 全平台 + 私有 |

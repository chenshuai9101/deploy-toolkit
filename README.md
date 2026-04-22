# deploy-toolkit - AI Agent 部署工具包

> 统一的 AI Agent 部署工具，支持多平台部署、自动化运维和 DevOps 工作流

## 核心功能

| 功能 | 说明 | CLI 命令 |
|------|------|----------|
| **应用部署** | 一键部署应用到主流云平台 | `deploy app deploy` |
| **容器编排** | Docker/Kubernetes 编排管理 | `deploy container` |
| **CI/CD 流水线** | 自动化构建和发布 | `deploy pipeline` |
| **监控告警** | 实时监控和智能告警 | `deploy monitor` |
| **配置管理** | 配置文件版本化管理 | `deploy config` |

## 快速开始

### 安装

```bash
npm install -g deploy-toolkit-cli
# 或
pip install deploy-toolkit
```

### 认证配置

```bash
deploy auth --provider aws --access-key <key> --secret-key <secret>
deploy auth --provider gcp --service-account <json-path>
deploy auth --provider azure --subscription-id <id>
```

### 基础用法

```bash
# 部署应用
deploy app deploy --name my-app --target production --platform aws

# 查看部署状态
deploy app status --name my-app

# 回滚版本
deploy app rollback --name my-app --version v1.2.3

# 管理容器
deploy container up --file docker-compose.yml
deploy container scale --service api --replicas 3

# CI/CD 流水线
deploy pipeline create --name ci-cd --repo https://github.com/user/repo
deploy pipeline run --name ci-cd --branch main

# 监控告警
deploy monitor status --service my-app
deploy monitor alert --rule cpu-usage --threshold 80
```

## 统一 CLI 接口

### 命令格式

```bash
deploy <resource> <action> [options] --json
```

### 全局选项

| 选项 | 说明 | 默认值 |
|------|------|--------|
| `--json` | 输出 JSON 格式 | false |
| `--verbose` | 详细日志模式 | false |
| `--timeout` | 超时时间(秒) | 300 |
| `--profile` | 部署环境配置 | default |

## 支持的平台

| 平台 | 支持状态 | 说明 |
|------|----------|------|
| AWS | ✅ 完全支持 | EC2, ECS, EKS, Lambda, S3 |
| GCP | ✅ 完全支持 | GCE, GKE, Cloud Run, Functions |
| Azure | ✅ 完全支持 | VM, AKS, App Service, Functions |
| Kubernetes | ✅ 完全支持 | 通用 K8s 集群 |
| Docker | ✅ 完全支持 | Docker Compose, Swarm |
| Vercel | ✅ 完全支持 | 前端应用部署 |
| Netlify | ✅ 完全支持 | JAMstack 部署 |

## Python SDK

```python
from deploy_toolkit import DeployToolkit

dt = DeployToolkit(api_key="your-api-key")

# 部署应用
result = dt.app.deploy(
    name="my-app",
    target="production",
    platform="aws",
    config={
        "instance_type": "t3.medium",
        "region": "us-east-1"
    }
)

# 查看状态
status = dt.app.status(name="my-app")
print(f"部署状态: {status.state}")

# 回滚
dt.app.rollback(name="my-app", version="v1.2.3")
```

## Node.js SDK

```javascript
import { DeployToolkit } from 'deploy-toolkit-sdk';

const dt = new DeployToolkit({ apiKey: process.env.DEPLOY_API_KEY });

// 部署应用
const result = await dt.app.deploy({
    name: 'my-app',
    target: 'production',
    platform: 'aws'
});

// 监控部署进度
result.on('progress', (data) => {
    console.log(`部署进度: ${data.percentage}%`);
});

result.on('complete', (data) => {
    console.log(`部署完成: ${data.endpoint}`);
});
```

## 输出格式

### JSON 结构

```json
{
  "success": true,
  "command": "app.deploy",
  "data": {
    "app_id": "app_abc123",
    "name": "my-app",
    "status": "deployed",
    "endpoint": "https://my-app.example.com",
    "version": "v1.0.0",
    "region": "us-east-1"
  },
  "meta": {
    "duration": 45234,
    "cost": 0.05,
    "version": "1.0.0"
  }
}
```

## 无状态设计

deploy-toolkit 采用无状态架构：

- **幂等操作**: 相同配置产生相同结果
- **可重复部署**: 支持同一配置的多次部署
- **状态追踪**: 所有部署状态持久化存储
- **审计日志**: 完整的操作审计记录

## 定价

| 套餐 | 价格 | 功能 |
|------|------|------|
| Free | $0 | 10次部署/月 + 1平台 |
| Pro | $19.99/月 | 无限部署 + 多平台 + CI/CD |
| Enterprise | 定制 | 私有部署 + SLA + 支持 |

## 文档

- [使用示例](./examples/)
- [模板库](./templates/)
- [API 文档](https://docs.deploy-toolkit.dev)

## 许可证

MIT License - 详见 [LICENSE](./LICENSE) 文件

## 贡献

欢迎提交 Issue 和 Pull Request！

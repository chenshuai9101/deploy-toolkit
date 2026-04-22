# 基础部署模板

## 使用方法

```bash
deploy app deploy --template basic --name <app-name>
```

## 配置项

| 参数 | 说明 | 默认值 |
|------|------|--------|
| `name` | 应用名称 | 必需 |
| `platform` | 部署平台 | aws |
| `instance_type` | 实例类型 | t3.micro |
| `region` | 区域 | us-east-1 |

## 示例

```bash
deploy app deploy --template basic --name my-app --platform gcp
```

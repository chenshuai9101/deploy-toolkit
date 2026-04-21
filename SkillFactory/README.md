# SkillFactory

> AI Agent Skill 创作工具包 - 让 AI 能够自我进化、创建新技能

## 简介

SkillFactory 是一个"元技能"（Meta-Skill），它帮助 AI Agent 根据用户需求自动创建新的 Skill。无论是文档处理、数据分析、自动化操作还是创意生成，SkillFactory 都能快速构建符合规范的 Skill 包。

## 核心功能

### 🚀 智能生成
根据自然语言需求，自动生成完整的 Skill 结构：
- SKILL.md 核心文档
- README.md 用户指南
- examples/ 使用示例
- templates/ 模板资源

### ✅ 结构验证
自动检查 Skill 结构是否符合规范：
- 文件完整性
- 格式正确性
- 字段完整性
- 示例可用性

### 📦 发布支持
生成 Marketplace 上架所需的全部文件：
- METADATA.json 元数据
- INSTALL.md 安装指南
- CHANGELOG.md 变更日志

## 快速开始

### 用户请求创建 Skill

```
用户: 我需要一个处理图片的 Skill
```

AI Agent 调用 SkillFactory，自动生成：
```
ImageHandler/
├── SKILL.md
├── README.md
└── examples/
    └── basic.md
```

## 目录结构

```
SkillFactory/
├── SKILL.md              # 核心技能文档（AI 使用）
├── README.md             # 用户说明文档
├── examples/             # 使用示例
│   └── example1.md
└── templates/            # Skill 模板
    └── skill_template.md
```

## 最佳实践

1. **命名规范**：使用英文命名，简洁明确
2. **描述清晰**：一句话说明核心价值
3. **示例完备**：提供可运行的示例代码
4. **结构规范**：遵循 SkillFactory 目录规范

## 技术栈

- Markdown 文档格式
- 标准 Skill 目录结构
- JSON 元数据格式

## License

MIT License

# Skill 创建模板

复制此模板创建新的 Skill：

```markdown
# {Skill名称}

> {一句话描述核心功能}

## 概述
{详细描述，2-3句话说明这个 Skill 的用途和使用场景}

## 触发条件
{什么情况下应该使用这个 Skill}
- 用户请求 {具体场景}
- 需要 {具体功能}

## 核心能力
### 1. 能力名称
- 功能说明
- 输入：{参数及格式}
- 输出：{返回结果格式}

### 2. 能力名称
- 功能说明

## 使用方法

### 基本用法
\`\`\`
{示例代码或命令}
\`\`\`

### 进阶用法
\`\`\`
{更复杂的使用示例}
\`\`\`

## 工具依赖
- {工具1}
- {工具2}

## 限制说明
- 限制1
- 限制2

## 最佳实践
- 建议1
- 建议2

## 相关资源
- [相关文档链接]
- [示例代码]

## 版本历史
- v1.0 ({日期}): 初始版本
```

---

## 目录结构模板

```
SkillName/
├── SKILL.md              # 核心文档
├── README.md             # 用户指南
├── examples/             # 示例目录
│   ├── basic.md          # 基础示例
│   └── advanced.md       # 进阶示例
├── templates/            # 模板目录
│   └── template.md       # 模板文件
└── scripts/              # 脚本目录（如需要）
    └── helper.py         # 辅助脚本
```

---

## METADATA.json 模板

```json
{
  "name": "skill-name",
  "version": "1.0.0",
  "description": "一句话描述",
  "author": "作者名称",
  "tags": ["tag1", "tag2"],
  "license": "MIT",
  "homepage": "https://github.com/user/repo",
  "keywords": ["keyword1", "keyword2"],
  "runtime": {
    "platform": "coze",
    "requires": ["tool1", "tool2"]
  }
}
```

# SkillFactory - AI Agent Skill Creation Toolkit

> **元技能**：帮助 AI Agent 自主创建、验证和发布新 Skill 的工厂工具

## 概述

SkillFactory 是"元技能"（Meta-Skill），它赋予 AI Agent **自我进化的能力**——不仅能执行任务，还能根据需求创建新的工具技能。当用户需要特定功能但系统中没有对应 Skill 时，SkillFactory 可以自动生成。

---

## 核心能力

### 1. 智能生成 SKILL.md

根据用户需求描述，自动生成符合规范的 Skill 核心文档：

```markdown
- 分析需求场景
- 提取核心功能
- 设计工具接口
- 编写使用指南
```

### 2. 脚手架构建

自动创建完整的 Skill 目录结构：

```
SkillName/
├── SKILL.md          # 核心技能文档
├── README.md         # 用户说明
├── examples/         # 使用示例
│   └── demo.md
├── templates/        # 模板资源
│   └── template.md
└── scripts/          # 辅助脚本（如有）
```

### 3. 结构验证

验证生成的 Skill 是否满足规范：

| 检查项 | 说明 |
|--------|------|
| 文件完整性 | 必需文件是否存在 |
| 格式规范 | Markdown 格式是否正确 |
| 字段齐全 | SKILL.md 必填字段是否完整 |
| 示例可用 | 示例代码是否可执行 |

### 4. 发布清单生成

生成 Skill 上架 Marketplace 所需的清单文件：

- `METADATA.json` - Skill 元数据
- `INSTALL.md` - 安装指南
- `CHANGELOG.md` - 变更日志模板

---

## 使用方法

### 场景 1：用户需要创建新 Skill

当用户请求创建特定功能的 Skill 时：

```
用户: 我需要一个处理 Excel 文件的 Skill
```

SkillFactory 自动执行：

1. **分析需求**
   - 确定 Skill 类型：数据处理
   - 识别核心功能：Excel 读取、编辑、公式、图表
   - 评估依赖工具：excel_master 技能

2. **生成结构**
   - 创建目录
   - 编写 SKILL.md
   - 编写 README.md
   - 创建示例

3. **输出结果**
   ```
   已创建 ExcelPro Skill:
   ├── SKILL.md
   ├── README.md
   └── examples/
       └── basic.md
   ```

### 场景 2：验证现有 Skill

用户提交 Skill 进行审核：

```
skill_factory.validate("./用户提交的Skill/")
```

返回验证报告：
```
✅ 文件完整性: 通过
✅ 格式规范: 通过  
✅ 字段齐全: 通过
⚠️ 示例可用: 发现问题 - 示例路径错误
```

---

## 最佳实践

### SKILL.md 必填字段

```yaml
skill_name:          # 唯一标识，英文+下划线
description:         # 一句话描述，50字内
core_capabilities:   # 核心能力列表
  - 能力1
  - 能力2
tools_required:      # 依赖的工具列表
usage_patterns:     # 使用模式
trigger_conditions:  # 触发条件
```

### Skill 命名规范

- **英文优先**：使用英文命名，便于国际化
- **简洁明确**：`pdf` 优于 `document_processor`
- **驼峰可选**：`skillFactory` 或 `skill_factory` 均可
- **避免冲突**：检查与现有 Skill 不重名

### 目录结构规范

```
SkillName/
├── SKILL.md          # 必须：核心文档
├── README.md         # 必须：用户说明
├── examples/         # 可选：至少1个示例
│   └── *.md
├── templates/        # 可选：模板资源
│   └── *.md
└── scripts/          # 可选：脚本文件
    └── *.py
```

---

## Skill 生成模板

```markdown
# {Skill名称}

> {一句话描述}

## 概述
{详细描述，2-3句话}

## 核心能力
- 能力1：{说明}
- 能力2：{说明}

## 使用方法
### 基本用法
```
{示例代码}
```

## 限制说明
- 限制1
- 限制2

## 相关资源
- 参考文档链接
```

---

## 技术细节

### 依赖项
- 文件系统读写能力
- Markdown 解析能力
- 模板引擎（如 jinja2）

### 输出格式
- SKILL.md: Markdown 格式
- README.md: Markdown 格式
- 示例: Markdown 格式

---

## 发布流程

1. **本地创建**：使用 SkillFactory 生成 Skill
2. **本地验证**：运行 `validate()` 确保结构正确
3. **生成清单**：自动生成发布所需文件
4. **推送到 GitHub**：提交到 skill-factory 仓库
5. **Marketplace 上架**：审核通过后发布

---

## 版本历史

- v1.0 (2025-01-21): 初始版本，支持基本生成和验证

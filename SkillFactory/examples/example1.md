# SkillFactory 使用示例

## 示例 1：创建文档处理 Skill

### 用户需求
> 我需要一个处理 PDF 文件的 Skill，能提取文本、合并多个 PDF、添加水印

### SkillFactory 执行过程

```markdown
## 1. 需求分析
- Skill 类型: 文档处理
- 核心功能: PDF 文本提取、合并、水印
- 复杂度: 中等

## 2. 生成的 Skill 结构
PDFProcessor/
├── SKILL.md          # 核心文档
├── README.md         # 用户指南
└── examples/
    └── basic.md      # 使用示例

## 3. 生成的 SKILL.md 内容
# PDFProcessor
> PDF document processing toolkit

## 核心能力
- extract: 从 PDF 提取文本和图片
- merge: 合并多个 PDF 文件
- watermark: 添加文字或图片水印

## 使用方法
### 提取文本
使用 pdf 技能的 parse_file 工具...
```

---

## 示例 2：创建社交媒体 Skill

### 用户需求
> 帮我创建一个自动发布小红书笔记的 Skill

### 生成的 Skill 片段

```markdown
# XiaoHongShu Publisher

> 一键发布小红书笔记，支持图片和文案

## 触发条件
用户请求发布小红书、分享到小红书、创建小红书笔记

## 核心能力
- post(): 发布笔记
- upload_image(): 上传图片
- get_stats(): 获取数据统计

## 使用限制
- 需要配置小红书 cookies
- 每日发布上限 10 篇
```

---

## 示例 3：验证 Skill 结构

### 输入
```
skill_factory.validate("./用户提交的Skill/")
```

### 输出
```json
{
  "status": "passed",
  "checks": {
    "file_completeness": true,
    "format_validation": true,
    "required_fields": true,
    "examples_available": true
  },
  "score": 95,
  "warnings": [
    "建议添加 templates/ 目录"
  ]
}
```

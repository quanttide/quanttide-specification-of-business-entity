---
title: 量潮科技智能体技能标准
---

# 智能体技能

本文档定义量潮科技智能体技能（Skill）的格式规范，遵循 [Agent Skills](https://github.com/agentskills/agentskills) 开放标准。

## 目录结构

技能是一个目录，至少包含 `SKILL.md` 文件：

```
skill-name/
├── SKILL.md          # 必需：元数据 + 指令
├── scripts/          # 可选：可执行代码
├── references/       # 可选：参考资料
├── assets/           # 可选：静态资源
└── ...               # 其他文件或目录
```

## SKILL.md 格式

`SKILL.md` 文件必须包含 YAML 头部元数据，后跟 Markdown 内容。

### 头部元数据

| 字段 | 必需 | 约束 |
|------|------|------|
| name | 是 | 最多 64 字符。仅小写字母、数字、连字符。不能以连字符开头或结尾。 |
| description | 是 | 最多 1024 字符。非空。描述技能功能和使用场景。 |
| version | 否 | 版本号，遵循语义化版本规范。 |
| author | 否 | 作者名称或组织。 |
| license | 否 | 许可证名称。 |
| compatibility | 否 | 最多 500 字符。环境要求（目标产品、系统包、网络访问等）。 |
| tags | 否 | 标签列表，用于分类和检索。 |

### name 字段

必填字段：
- 长度 1-64 字符
- 仅包含小写字母（a-z）和连字符（-）
- 不能以连字符开头或结尾
- 不能包含连续连字符（--）
- 必须与父目录名称匹配

### description 字段

必填字段：
- 长度 1-1024 字符
- 应描述技能功能和使用场景
- 应包含关键词，帮助智能体识别相关任务

### version 字段

可选字段：
- 遵循语义化版本规范：`主版本.次版本.修订号`
- 例如：`1.0.0`、`0.1.0`

### tags 字段

可选字段：
- 技能标签列表
- 用于分类和检索
- 示例：`["docs", "writing", "format"]`

### 正文内容

Markdown 正文包含技能指令。参考[文档格式标准](../docs/format.md)进行写作。

推荐章节：
- 概述：技能简介和使用场景
- 指令：分步骤操作说明
- 示例：输入输出示例
- 注意事项：常见问题和边界情况

注意：智能体激活技能时会加载整个 `SKILL.md` 文件。内容过长时，考虑拆分到引用文件。

## 可选目录

### scripts/

包含智能体可执行的代码脚本。

要求：
- 自包含或明确标注依赖
- 包含有用的错误信息
- 优雅处理边界情况

常用语言：Python、Bash、JavaScript

### references/

包含智能体按需读取的参考资料：

- `REFERENCE.md` - 详细技术参考
- `FORMS.md` - 表单模板或结构化数据格式
- 领域特定文件（`finance.md`、`legal.md` 等）

保持引用文件聚焦。智能体按需加载，文件越小占用的上下文越少。

### assets/

包含静态资源：
- 模板（文档模板、配置模板）
- 图片（图表、示例）
- 数据文件（查询表、schema）

## 渐进式披露

技能应针对高效的上下文使用进行结构化：

1. **元数据**（约 100 tokens）：启动时加载所有技能的 `name` 和 `description`
2. **指令**（建议 < 5000 tokens）：激活技能时加载完整 `SKILL.md` 正文
3. **资源**（按需）：文件（如 `scripts/`、`references/`、`assets/`）仅在需要时加载

保持主 `SKILL.md` 在 500 行以内。将详细参考资料移至独立文件。

## 文件引用

引用技能内其他文件时，使用相对于技能根目录的路径：

```markdown
详见 [参考指南](references/REFERENCE.md)

运行提取脚本：
scripts/extract.py
```

文件引用保持从 `SKILL.md` 向下一级。避免深层嵌套的引用链。

## 命名规范

- 目录名： kebab-case（短横线命名）
- 文件名： kebab-case
- 避免使用中文名称

## 验证工具

使用 [skills-ref](https://github.com/agentskills/agentskills/tree/main/skills-ref) 参考库验证技能：

```bash
skills-ref validate ./my-skill
```

这会检查 `SKILL.md` 头部元数据有效并遵循所有命名规范。

## 示例

```yaml
---
name: docs-formatter
description: 格式化文档，确保遵循量潮科技文档格式标准。适用于 Markdown 文件的规范化处理。
version: 1.0.0
author: 量潮科技
license: MIT
tags:
  - docs
  - format
  - markdown
---

## 概述

此技能用于格式化 Markdown 文档，确保符合文档格式标准。

## 使用场景

- 规范化现有文档格式
- 新文档格式检查
- 批量处理多个文件

## 指令

1. 读取文档内容
2. 检查格式问题
3. 应用格式化规则
4. 保存修改

## 示例

输入：未格式化的 Markdown
输出：符合标准的格式化文档
```

## 相关规范

- [文档格式标准](../docs/format.md)
- [版本发布标准](../devops/release.md)
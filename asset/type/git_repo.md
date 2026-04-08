# Git 仓库资产管理

## 概述

以标准资产体系为准，GitHub 优先，围绕 GitHub 建立生态。

量潮数据、量潮课堂可以在量潮的标准资产体系里额外有自己的资产，比如数据处理器。

## 仓库级文件规范

### 文件清单

| 文件 | 用途 | 必选 |
|------|------|------|
| `README.md` | 项目概述、目录结构 | 是 |
| `CONTRIBUTING.md` | 贡献指南、工作流、环境变量 | 是 |
| `AGENTS.md` | Agent 导航 | 是 |
| `CHANGELOG.md` | 版本历史 | 是 |
| `.gitignore` | Git 忽略规则 | 是 |

### AI认知视角

三个核心文件对应AI的不同认知层次：

- **README.md - 陈述型记忆**：记录事实性知识，如项目是什么、有什么功能、如何使用
- **CONTRIBUTING.md - 程序型记忆**：记录操作流程，如如何开发、如何测试、如何发布
- **AGENTS.md - 元认知**：AI对自身的认知，知道有什么知识、在哪里、如何使用

### README.md

项目概述，包含：
- 项目简介（一句话）
- 目录结构
- 快速开始

### CONTRIBUTING.md

详细工作流文档，包含：
- 项目结构说明
- 开发环境配置
- 提交规范
- 发布流程
- 环境变量维护规则
- 人机协作原则

### AGENTS.md

Agent 导航文档（简洁 ~50 行），包含：

```markdown
# AGENTS.md

## 相关文档

| 文档 | 用途 |
|------|------|
| [README](README.md) | 项目概述、子模块列表 |
| [CONTRIBUTING](CONTRIBUTING.md) | 人机协作、子模块工作流、发布流程、环境变量 |
| [meta/IDENTITY.md](meta/IDENTITY.md) | 仓库自我映射、子模块列表 |
| [meta/SOUL.md](meta/SOUL.md) | AI 自我认知（自维护）|
| [meta/TOOLS.md](meta/TOOLS.md) | 工具清单（自维护）|

---

## 快速索引

| 任务 | 操作位置 |
|------|---------|
| 修改子模块 | CONTRIBUTING > 子模块工作流 |
| 发布 Release | CONTRIBUTING > 主仓库发布 Release |
| 提交变更 | `cz commit` |
| 处理错误 | CONTRIBUTING > 常见错误处理 |
| 更新环境变量 | CONTRIBUTING > 环境变量 |
| 记录日报 | `meta/report/YYYY-MM-DD.md` |

---

## 协作原则

- 最小干预：仅用户明确请求时操作
- 原子提交：每次提交独立完整
- 验证优先：修改后运行构建验证

## 重要提示

- **子模块操作前先 checkout main**：`git checkout main && git pull`
- **读取 .env 需要临时权限**：Agent 无法直接读取 .env
- **自动同步**：.env 变更时同步更新 .env.example
- **Release 标题**：使用 `项目名/vX.Y.Z` 格式（如 cli/v0.0.1-alpha.3）
- **Release notes**：只包含对应版本内容

---

## 如何维护 AGENTS.md

| 类型 | 写在哪里 |
|------|---------|
| 详细说明、工作流步骤 | CONTRIBUTING |
| 给链接、导航索引 | AGENTS.md |

更新时机：新增文档、新增任务类型、重要规则变化时更新；README/CONTRIBUTING 已有的内容不重复。
```

**规范要点**：
- 使用场景表格（相关文档）
- 快速索引表格
- 协作原则（3 条）
- 重要提示（5 条）
- 如何维护 AGENTS.md

### CHANGELOG.md

版本变更记录，格式：

```markdown
# Changelog

## [版本号] - 日期

### Added
### Changed
### Fixed
### Removed
```

## Git使用规范

Git提交规范参见[devops/git.md](../../devops/git.md)

## 子模块维护

### 提交流程

```bash
# 1. 进入子模块
cd <子模块名>

# 2. 提交更改（使用 commitizen）
cz commit

# 3. 推送子模块
git push origin main

# 4. 返回主仓库更新引用
cd ..
git add <子模块名>
git commit -m "chore: update <子模块名> submodule"
git push origin main
```

### 同步远程更新

```bash
# 同步指定子模块到远程最新
git submodule update --remote <子模块名>
git add <子模块名>
cz commit -m "chore: update <子模块名> submodule"
git push origin main
```

## 最佳实践

1. **原子提交** - 每次提交独立完整，包含单一逻辑变更
2. **规范格式** - 使用 Conventional Commits 格式
3. **及时推送** - 本地提交后尽快推送到远程
4. **子模块同步** - 更新子模块后，立即同步父仓库引用
5. **版本标记** - 发布时使用语义化版本号
6. **CHANGELOG 维护** - 每次发布更新 CHANGELOG.md

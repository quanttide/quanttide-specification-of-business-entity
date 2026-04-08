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
| `meta/` | 元数据目录 | 可选 |
| `.gitignore` | Git 忽略规则 | 是 |

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

## Git 提交规范

### 默认工具：commitizen

使用 `commitizen` 生成符合 Conventional Commits 规范的 commit message。

**基本用法：**
```bash
# 交互式创建规范提交
cz commit
# 或简写
cz c

# 自动版本升级 + 生成 CHANGELOG
cz bump
```

**Commit 类型：**

| 类型 | 说明 | 示例 |
|------|------|------|
| `feat` | 新功能 | `feat: add user authentication` |
| `fix` | 修复 bug | `fix: resolve null pointer exception` |
| `docs` | 文档更新 | `docs: update README` |
| `test` | 测试相关 | `test: add unit tests for api` |
| `refactor` | 代码重构 | `refactor: simplify logic` |
| `chore` | 构建/工具 | `chore: update dependencies` |

### 手动提交格式

当无法使用 `cz commit` 时（如脚本、CI 环境），手动遵循格式：

```bash
git commit -m "<type>: <description>"
```

## 版本发布规范

### Tag vs Release 命名

| 方面 | Git Tag | GitHub Release |
|------|-----|---------|
| 命名 | 加 `v` 前缀，符合 semver | 与 Git Tag 一致 |
| 用途 | Git 引用 | 用户可见 |
| 示例 | `v0.1.0` 或 `cli/v0.1.0` | `v0.1.0` 或 `cli/v0.1.0` |

创建 Git Tag 后，同步创建 GitHub Release，Tag Name 与 Git Tag 一致。

### Monorepo 标签规范

对于 monorepo 项目（如 qtadmin），使用 `项目名/v+版本号` 格式：

```bash
# provider 发布
git tag provider/v0.0.1
git push origin provider/v0.0.1

# cli 发布
git tag cli/v0.0.1
git push origin cli/v0.0.1
```

### 发布流程

1. **更新 CHANGELOG.md** - 在对应项目目录下添加新版本和变更内容
2. **提交 CHANGELOG.md** - 使用 `cz commit` 或手动提交
3. **创建标签** - `git tag <project>/v<version>`
4. **推送标签** - `git push origin <project>/v<version>`
5. **创建 Release** - 使用 `gh release create` 或 GitHub 界面
   - Release Tag: `<project>/v<version>`（与 Git Tag 一致）
   - Release 标题：`<project>/v<version>`

```bash
# 示例：cli 发布
git tag cli/v0.0.1-alpha.4
git push origin cli/v0.0.1-alpha.4
gh release create cli/v0.0.1-alpha.4 --title "cli/v0.0.1-alpha.4" --notes "Release notes..."
```

### 版本规范

遵循语义化版本（SemVer）：
- alpha: `v0.0.1-alpha.1`
- beta: `v0.0.1-beta.1`
- release: `v0.0.1`

### 常见错误

**问题**：Release Tag 与 Git Tag 不一致

例如：Git Tag 使用 `cli/v0.0.1-alpha.4`，但 GitHub Release 使用 `v0.0.1-alpha.4`

**原因**：
1. 混淆了单仓项目与独立仓库的发布规范
2. 误以为 GitHub Release 的 Tag 应该去掉项目前缀
3. 文档规范不够明确

**正确做法**：
```bash
# Git Tag（带项目前缀）
git tag cli/v0.0.1-alpha.4
git push origin cli/v0.0.1-alpha.4

# GitHub Release（与 Git Tag 一致）
gh release create cli/v0.0.1-alpha.4 --title "cli/v0.0.1-alpha.4" --notes "..."
```

**关键原则**：GitHub Release 的 Tag Name 必须与 Git Tag 完全一致，这样 GitHub 才能正确关联 Release 和 Git Tag。

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

### 防坑校验：推送前检查

**问题**：父仓库推送了一个指向未推送的子模块 commit，导致其他人无法克隆。

**规则**：在父仓库 push 之前，确保所有子模块已先于父仓库执行 git push。

**检查脚本**：
```bash
# 检查子模块是否有未推送的提交
git submodule foreach '
  if [ "$(git rev-list HEAD..origin/main --count 2>/dev/null || echo 0)" != "0" ]; then
    echo "⚠️  $name 有未推送的提交，请先推送"
    exit 1
  fi
'

# 或使用 Python 脚本自动检查
python scripts/commit_submodules.py --dry-run
```

**推荐工作流**：
1. 在子模块中完成提交并推送
2. 返回父仓库更新子模块引用
3. 推送父仓库前运行检查脚本
4. 确认所有子模块已推送后，再推送父仓库

## 最佳实践

1. **原子提交** - 每次提交独立完整，包含单一逻辑变更
2. **规范格式** - 使用 Conventional Commits 格式
3. **及时推送** - 本地提交后尽快推送到远程
4. **子模块同步** - 更新子模块后，立即同步父仓库引用
5. **版本标记** - 发布时使用语义化版本号
6. **CHANGELOG 维护** - 每次发布更新 CHANGELOG.md

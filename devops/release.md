# 版本发布规范

本文档定义量潮科技项目的版本发布流程和规范。

## 版本号规范

遵循语义化版本（Semantic Versioning）规范：`主版本.次版本.修订号`

### 版本号规则

- **主版本（Major）**：不兼容的API修改
- **次版本（Minor）**：向后兼容的功能新增
- **修订号（Patch）**：向后兼容的问题修复

### 示例

- `v1.0.0`：首个正式版本
- `v1.1.0`：新增功能
- `v1.0.1`：修复bug
- `v2.0.0`：重大架构调整

## 发布流程

### 准备阶段

1. **检查未发布内容**：
   ```bash
   git log <last-version>..HEAD --oneline
   ```

2. **确认代码质量**：
   - 所有测试通过
   - 文档已更新
   - 无未提交的变更

### CHANGELOG更新

1. **编辑CHANGELOG.md**：
   ```markdown
   # CHANGELOG
   
   ## [Unreleased]
   
   ## [<version>] - <date>
   
   ### Added
   - 新增功能列表
   
   ### Changed
   - 修改内容列表
   
   ### Fixed
   - 修复问题列表
   
   ### Removed
   - 移除内容列表
   ```

2. **提交CHANGELOG更新**：
   ```bash
   git add CHANGELOG.md
   git commit -m "chore: update CHANGELOG for <version>"
   git push origin main
   ```

### 创建标签

1. **创建Git标签**：
   ```bash
   git tag <version>
   ```

2. **推送标签到远程**：
   ```bash
   git push origin <version>
   ```

### 创建GitHub Release

使用GitHub CLI创建Release：

```bash
gh release create <version> \
  --title "<version>" \
  --generate-notes
```

### 更新Release Notes

通过API更新Release内容：

```bash
gh api repos/<owner>/<repo>/releases/<release-id> \
  -X PATCH \
  -f body="<release-notes>"
```

Release notes应从CHANGELOG中提取对应版本的内容。

## CHANGELOG规范

### 格式要求

- 使用Markdown格式
- 每个版本独立章节
- 使用日期标注：`YYYY-MM-DD`
- 使用分类标签：Added、Changed、Fixed、Removed

### 内容要求

- 简洁明了，避免冗余描述
- 使用动词开头：「新增」「修改」「修复」「移除」
- 每条记录一行，不超过50字
- 按重要性排序

### 示例

```markdown
## [v0.0.3] - 2026-04-08

### Added
- 新增写作格式规范

### Changed
- 重命名文档文件
- 修正发布流程

### Fixed
- 合并冗余文档
```

## Git标签规范

### 标签命名

- 使用版本号作为标签名：`v1.0.0`
- 格式：`v` + 主版本 + `.` + 次版本 + `.` + 修订号

### 标签类型

- **轻量标签**：用于临时标记
- **附注标签**：用于正式发布（推荐）

创建附注标签：
```bash
git tag -a v1.0.0 -m "Release version 1.0.0"
```

## GitHub Release规范

### 标题规范

- 格式统一：`v<version>`
- 示例：`v0.0.1`、`v0.0.2`、`v0.0.3`

### Release Notes规范

- 内容来源：从CHANGELOG提取
- 使用标准分类：Added、Changed、Fixed、Removed
- 遵循文档格式规范（参见docs/format.md）
- 避免使用引号装饰普通术语

### 标记规范

- Latest：最新稳定版本
- Pre-release：预发布版本（如alpha、beta）

## 发布检查清单

发布前确认以下事项：

- [ ] CHANGELOG已更新
- [ ] 版本号符合语义化版本规范
- [ ] Git标签已创建并推送
- [ ] GitHub Release已创建
- [ ] Release notes内容准确
- [ ] 主仓库子模块引用已更新

## 常见问题

### 如何修改已发布的Release？

通过GitHub API修改：
```bash
gh api repos/<owner>/<repo>/releases/<release-id> \
  -X PATCH \
  -f name="<new-title>" \
  -f body="<new-content>"
```

### 如何删除错误的标签？

```bash
# 删除本地标签
git tag -d <version>

# 删除远程标签
git push origin --delete <version>
```

### 如何查看历史Release？

```bash
# 查看Release列表
gh release list

# 查看特定Release
gh release view <version>
```

## 参考文档

- [Semantic Versioning](https://semver.org/)
- [Keep a Changelog](https://keepachangelog.com/)
- [GitHub Releases](https://docs.github.com/en/repositories/releasing-projects-on-github)
# CHANGELOG

## [Unreleased]

## [0.1.1] - 2026-04-08

### Added

- 新增asset/category/handbook.md：手册资产规范

### Changed

- 重构手册资产规范结构：合并为概述和写作规范两个章节

## [0.1.0] - 2026-04-08

### Added

- 新增ROADMAP.md：项目路线图和待完善领域
- 新增.gitignore：过滤Jupyter Book和Python编译文件
- 新增devops/git.md：Git使用规范和子模块维护
- 新增devops/release.md：版本发布规范
- 新增asset/category/specification.md：工程标准资产规范
- 新增AI认知视角说明：README.md、CONTRIBUTING.md、AGENTS.md的认知层次

### Changed

- 重构git_repo.md：分离文件清单和内容规范，强调保留文件概念
- 整理AGENTS.md和CONTRIBUTING.md：简化并引用规范文档
- 完善README.md：添加目录结构和快速开始
- 重写工程标准资产规范：基于实际经验，包含创建、维护、废弃流程
- 移动Git使用和子模块规范到devops/git.md
- 移动版本发布规范到devops/release.md
- 调整发布流程结构：合并重复章节，移除FAQ

### Removed

- 删除发布规范中的FAQ章节
- 删除git_repo.md中的git使用规范（已移到devops/git.md）

## [0.0.3] - 2026-04-08

### Added

- 新增写作格式规范：write/format.md
- 新增引号使用规范：docs/format.md 引号章节

### Changed

- 重命名 write/format.md 到 docs/format.md
- 修改标题：从"写作格式标准"改为"文档格式标准"
- 修正 CONTRIBUTING.md 发布流程顺序和命令
- 更新记忆系统文档

### Fixed

- 合并 monorepo.md 到 git_repo.md

## [0.0.2] - 2026-04-02

### Changed

- 重构项目目录结构
- 更新记忆系统文档（声明性记忆、程序性记忆）

## [0.0.1] - 2026-03-14

### Added

- 初始化 specification 子模块
- 新增 AGENTS.md：Agent 工作指南
- 新增 CONTRIBUTING.md：贡献指南
- 新增 meta/index.md：元标准定义
- 新增 default/memory/index.md：记忆系统定义
- 新增 default/memory/episodic.md：事件记忆规范

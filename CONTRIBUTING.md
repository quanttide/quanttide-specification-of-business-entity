# 贡献指南

欢迎贡献本项目！本文档提供贡献相关指南。

## 贡献方式

- 报告问题：通过 GitHub Issues 反馈
- 提交修改：通过 Pull Request 贡献代码或文档

## 文档规范

### 文件命名

- 使用小写字母
- 单词间用下划线 `_` 分隔
- 示例：`index.md`、`spec_name.md`

### 内容风格

- 使用简体中文
- 保持语言简洁、专业
- 使用 spec 风格：字段表格、枚举定义、示例代码

### 提交信息规范

- 使用中文描述更改内容
- 简洁明了

## 提交流程

1. **Fork 仓库**
2. **创建分支**：`git checkout -b feature/xxx` 或 `git checkout -b fix/xxx`
3. **进行修改**
4. **提交更改**
5. **推送分支**：`git push origin branch-name`
6. **创建 Pull Request**

## 发布流程

1. **检查 CHANGELOG**：查看已有版本记录格式
2. **更新 CHANGELOG**：在 `[Unreleased]` 下新增版本块
3. **提交推送**：确保所有变更已推送到远程
4. **创建 Release**：
   - `gh release create <version> --title "v<version>" --notes-file CHANGELOG.md`
5. **打标签**：`git tag <version>` && `git push origin <version>`

## 版本规范

遵循语义化版本（SemVer）：`主版本.次版本.修订号`

## 联系方式

如有疑问，可通过 GitHub Issues 联系维护者。

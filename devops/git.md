# Git使用规范

本文档定义Git提交和版本控制的使用规范。

## 提交规范

### 工具：commitizen

使用commitizen生成符合Conventional Commits规范的提交信息。

**基本用法：**
```bash
# 交互式创建规范提交
cz commit
# 或简写
cz c

# 自动版本升级 + 生成 CHANGELOG
cz bump
```

### 提交类型

| 类型 | 说明 | 示例 |
|------|------|------|
| `feat` | 新功能 | `feat: add user authentication` |
| `fix` | 修复bug | `fix: resolve null pointer exception` |
| `docs` | 文档更新 | `docs: update README` |
| `test` | 测试相关 | `test: add unit tests for api` |
| `refactor` | 代码重构 | `refactor: simplify logic` |
| `chore` | 构建/工具 | `chore: update dependencies` |

### 手动提交格式

当无法使用commitizen时（如脚本、CI环境），手动遵循格式：

```bash
git commit -m "<type>: <description>"
```

## 分支规范

### 分支命名

- `main`：主分支，稳定版本
- `feature/xxx`：功能分支
- `fix/xxx`：修复分支
- `release/xxx`：发布分支

### 分支操作

```bash
# 创建并切换分支
git checkout -b feature/xxx

# 切换回主分支
git checkout main

# 合并分支
git merge feature/xxx

# 删除分支
git branch -d feature/xxx
```

## 远程仓库操作

```bash
# 查看远程仓库
git remote -v

# 拉取最新代码
git pull origin main

# 推送到远程
git push origin main

# 推送标签
git push origin <tag-name>
```

## 最佳实践

1. **原子提交**：每次提交独立完整，包含单一逻辑变更
2. **规范格式**：使用Conventional Commits格式
3. **及时推送**：本地提交后尽快推送到远程
4. **拉取更新**：推送前先拉取远程更新，避免冲突
5. **子模块同步**：更新子模块后，立即同步父仓库引用
6. **版本标记**：发布时使用语义化版本号
7. **CHANGELOG维护**：每次发布更新CHANGELOG.md

## 子模块维护

### 提交流程

```bash
# 1. 进入子模块
cd <子模块名>

# 2. 提交更改（使用commitizen）
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

### 初始化子模块

```bash
# 初始化所有子模块
git submodule update --init --recursive

# 更新所有子模块到最新
git submodule update --remote
```

## .gitignore规范

### 用途

.gitignore文件用于指定Git应忽略的文件和目录，避免将不必要的文件提交到仓库。

### 常见过滤规则

**Jupyter Book项目**：
```gitignore
_build/
*.html
```

**Python项目**：
```gitignore
__pycache__/
*.py[cod]
*$py.class
venv/
.venv/
```

**Jupyter Notebook**：
```gitignore
.ipynb_checkpoints
```

**操作系统**：
```gitignore
.DS_Store
Thumbs.db
```

**编辑器**：
```gitignore
.vscode/
.idea/
*.swp
```

### 维护原则

- 根据项目类型配置对应规则
- 及时更新，避免提交无用文件
- 保持仓库整洁，只追踪必要的源文件

## 参考文档

- [Conventional Commits](https://www.conventionalcommits.org/)
- [Git官方文档](https://git-scm.com/doc)
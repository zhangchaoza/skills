---
name: git-commit
description: "Generates git commit messages based on the changes made in the code. When the user requests to generate commit message and make commits, use this skill."
license: MIT
metadata:
  author: zhangchao
  version: "1.1.0"
---

# 生成提交信息

够根据代码的变更内容, 生成清晰、简洁的提交信息。

## 步骤

### 步骤 1: 确定提交信息的类型

根据当前git暂存的变更内容，忽略未暂存的文件。确定提交信息的类型。类型参考以下说明:

```
提交类型: 本次提交的主要类型，从下面选择一个
- feat:     新功能
- fix:      修复 Bug
- docs:     文档变更
- style:    代码格式调整（不影响代码逻辑）
- refactor: 代码重构（既不是新功能，也不是修复 Bug）
- perf:     性能优化
- test:     添加或修改测试代码
- build:    构建系统或依赖项变更
- ci:       CI/CD 配置变更
- chore:    其他杂项（如更新构建脚本、配置文件等）
- revert:   撤销之前的提交
```

### 步骤 2: 生成提交信息

1. 根据变更内容，生成清晰、简洁的提交信息。
2. 可以添加详细描述，详细描述本次提交的背景、动机、实现细节等。可以使用多行文本，每行不要超过 72 个字符。
3. 可以添加关联 Issue（可选）。如果本次提交与某个 Issue 相关，请在这里列出
4. 如果用户没有额外说明，提交信息默认使用中文
5. 遵循以下格式:

```
<类型>: <简短描述>

详细描述（可选）
在这里可以详细描述本次提交的背景、动机、实现细节等。
可以使用多行文本，每行不要超过 72 个字符。

关联 Issue（可选）
如果本次提交与某个 Issue 相关，请在这里列出，格式为：
Closes #<Issue 编号>
```

**限制**: 不要在生成的提交信息中，添加一些标记说明。比如 `此信息由Claude生成` 或是 `Co-Authored-By: AtomCode (deepseek-v4-flash) <noreply@atomgit.com` 诸如此类的信息。

## 步骤 3: 创建提交信息

- 使用命令 `git commit -m "提交内容"` 提交代码到当前分支。
- 如果没有用户的额外说明，不允许推送到远端。

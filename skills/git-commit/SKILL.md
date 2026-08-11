---
name: git-commit
description: "Generates git commit messages based on the changes made in the code. When the user requests to generate commit message and make commits, use this skill."
license: MIT
metadata:
  author: zhangchao
  version: "1.2.0"
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
5. 遵循以下内容结构。注意：**内容结构只是信息层次，不是命令的书写方式**，提交命令的写法见「步骤 3」

```
<类型>: <简短描述>

详细描述（可选）
在这里可以详细描述本次提交的背景、动机、实现细节等。
可以使用多行文本，每行不要超过 72 个字符。

关联 Issue（可选）
如果本次提交与某个 Issue 相关，请在这里列出，格式为：
Closes #<Issue 编号>
```

**限制**:

- 不要在生成的提交信息中，添加一些标记说明。比如 `此信息由Claude生成` 或是 `Co-Authored-By: AtomCode (deepseek-v4-flash) <noreply@atomgit.com` 诸如此类的信息。
- **禁止使用 `@'...'@` 或 `@"..."@` 这类 PowerShell here-string 写法**。它会以 `@` 起始和结尾，并在真正的提交信息前产生多余空行，污染提交记录。

## 步骤 3: 创建提交信息

- 提交信息为**单行**时，直接使用内联字符串：
  ```
  git commit -m "feat: 新增字段禁用时自动清空其文本值"
  ```
- 提交信息为**多行**（含简短描述 + 空行 + 详细描述）时，优先使用**多个 `-m` 参数**，每个 `-m` 对应一个段落，段内用空格或换行自然衔接，段落之间用空字符串参数分隔：
  ```
  git commit \
    -m "feat: 字段禁用时自动清空其文本值" \
    -m "新增 AutoCleanAfterDisable 配置，当设置了该标志的文本框字段被禁用（IsEnabled 变为 false）时，自动清空其当前文本内容。" \
    -m "- ProductSettingField 新增 AutoCleanAfterDisable 属性" \
    -m "- GerenalSettingsGroupView 在字段禁用时清空文本框" \
    -m "Closes #123"
  ```
  这样每个 `-m` 会生成一个独立段落，段落间自动插入空行，无需手动拼接换行符。
- 在 **PowerShell** 中执行时，同理使用多个 `-m` 参数（可用反引号 `` ` `` 续行），不要使用 here-string：
  ```
  git commit -m "feat: 字段禁用时自动清空其文本值" -m "新增 AutoCleanAfterDisable 配置..."
  ```
- 每行字符数按「步骤 2」控制在 72 个以内；若某段文字过长，拆成多个 `-m`。
- 如果没有用户的额外说明，不允许推送到远端。

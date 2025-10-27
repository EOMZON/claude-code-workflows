# 使用说明（Claude Code Workflows）

本文档说明如何在你的项目中落地本仓库的三套工作流：代码审查、设计审查、安全审查。核心分两类用法：
- GitHub Actions 自动化：在 PR 上自动跑审查并回评。
- Claude Code 斜杠命令/子代理：在本地开发迭代中即时触发审查（/review、/security-review、/design-review）。

## 1. 前提条件
- 你有一个 GitHub 仓库，且已启用 GitHub Actions。
- 你的 IDE 已安装并登录 Claude Code（支持自定义 Slash Command 与 Subagent）。
- 若使用设计审查的「实时 UI 自动化」，需要配置 Playwright MCP（参考其 README）。

## 2. GitHub Actions 自动化（PR 自动审查）

将以下文件拷贝到你的项目 `.github/workflows/` 目录：
- 代码审查：`code-review/claude-code-review.yml` 或 `code-review/claude-code-review-custom.yml`
- 安全审查：`security-review/security.yml`

然后在 GitHub 仓库的 Settings → Secrets and variables → Actions 中设置密钥：
- 代码审查：`CLAUDE_CODE_OAUTH_TOKEN`（或 `CLAUDE_API_KEY`）
- 安全审查：`ANTHROPIC_API_KEY`

提交后，PR 在以下事件会自动触发审查（可在 YAML 中调整）：opened、synchronize、ready_for_review、reopened。

说明：YAML 中的 `prompt:` 已内置审查要求，无需额外命令。执行后，Bot 会在 PR 下方发布评论与进度。

## 3. 在 Claude Code 中配置斜杠命令与子代理（本地即时审查）

此方式适合你在本地完成一段改动后，想立即让 AI 审一遍再提交。

### 3.1 代码审查（推荐）
- 斜杠命令（Slash Command）：使用 `code-review/pragmatic-code-review-slash-command.md` 的内容创建一个命令，例如：`/review`。
- 子代理（Subagent）：使用 `code-review/pragmatic-code-review-subagent.md` 创建名为 `pragmatic-code-review` 的子代理。

使用方式：在 Claude Code 对话框输入：
```
/review
```
或直接让子代理执行（因 IDE 不同，操作入口可能是 @agent 或下拉选择）。

### 3.2 安全审查
- 斜杠命令：使用 `security-review/security-review-slash-command.md` 的内容创建命令，例如：`/security-review`。

使用方式：
```
/security-review
```

### 3.3 设计审查（含 Playwright MCP）
- 子代理：使用 `design-review/design-review-agent.md` 创建 `design-review` 代理。
- 斜杠命令：使用 `design-review/design-review-slash-command.md` 创建命令，例如：`/design-review`。
- 设计原则：将 `design-review/design-principles-example.md` 要点放入你仓库的 `CLAUDE.md` 或 `context/` 文档中，方便代理引用。
- 实时 UI 自动化：按 Playwright MCP 官方说明安装并在 Claude Code 中注册 MCP 服务器，以启用浏览器交互、截图与视口切换等能力。

使用方式：
```
/design-review
```

## 4. 常见目录与文件放置建议
- GitHub Actions（必需）：`.github/workflows/*.yml`（只能放这里才会触发）
- Prompt 模板（可选）：建议放 `docs/prompts/` 或 `context/` 目录集中管理；并在 `CLAUDE.md` 中链接它们。
- 你不需要把所有 Prompt 放在工程根目录；放根目录不会自动执行。Slash Command/子代理是在 Claude Code 内配置与调用。

## 5. 常用指令（在 Claude Code 中触发）
- 代码审查：`/review`
- 安全审查：`/security-review`
- 设计審查：`/design-review`

注意：这些是 Claude Code 的对话内命令，不是 shell/终端命令。

## 6. 自定义与进阶
- 修改审查标准：直接编辑各目录下的 `*.md`/`*.yml` 提示词或 Checklist，加入你团队的规范（如编码规范、架构风格、可访问性要求）。
- 调整工具权限：`allowed-tools` 字段定义了命令可用的工具，按需裁剪（例如是否允许调用 `gh pr comment`）。
- 模型与开关：在 YAML 的 `claude_args` 或安全审查 `security.yml` 中调整模型与额外参数。

## 7. 验证接入是否成功
- 提交任意 PR：应能看到「代码审查/安全审查」操作在 PR 上自动留言。
- 在 Claude Code：输入 `/review`、`/security-review`、`/design-review`，应得到结构化的审查报告。

## 8. 常见问题（FAQ）
**Q：Prompt 一定要放工程根目录吗？**
A：不需要。Prompt 是供 Claude Code 斜杠命令/子代理使用的模板，放根目录不会自动执行。建议放到 `docs/prompts/` 或 `context/`，并在 Claude Code 中配置引用。

**Q：GitHub Actions 为什么没有触发？**
- 确认工作流文件在 `.github/workflows/` 下。
- 确认 Secrets 名称与 YAML 内引用一致（如 `CLAUDE_CODE_OAUTH_TOKEN`、`ANTHROPIC_API_KEY`）。
- 确认触发条件（opened、synchronize 等）与当前动作匹配。

**Q：设计审查的浏览器操作为何不可用？**
- 需要安装并在 Claude Code 中注册 Playwright MCP，确保代理具备浏览器工具能力（截图、导航、视口切换等）。

---
如需我帮你把这些工作流直接嵌入你的目标仓库（含 Secrets 与命令配置），告诉我仓库结构与使用的 CI/IDE，我可代为落地与验收。


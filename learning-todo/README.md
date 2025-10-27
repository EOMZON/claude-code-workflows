# 功能完成后的本地审查 · 最小执行指南（Quick Start）

这是一份精简版操作单，保留必要步骤与指令，其他细节统一引用到对应文档，避免重复。

## 一、Quick Start（完成一个功能后的 5 步）
1) 启动与自检
   - Node 示例：`pnpm install && pnpm lint && pnpm test && pnpm dev`
   - Python 示例：`python -m venv .venv && . .venv/bin/activate && pip install -r requirements.txt && pytest -q && uvicorn app:app --reload --port 8000`
   - 端口可达：`curl -I http://127.0.0.1:3000`（改成你的端口）

2) 设计审查（Playwright MCP）
   - 在 IDE 对话框输入：`/dr http://127.0.0.1:3000/ http://127.0.0.1:3000/feature-x`
   - /dr 会自动执行 install → navigate → wait_for → screenshot → console/network/snapshot，并强制“证据优先”。

3) 代码审查（务实质量）
   - 在 IDE 对话框输入：`/cr`
   - 自动收集 git 上下文并输出 Summary / Critical / Improvements / Nits。

4) 安全审查（高置信度）
   - 在 IDE 对话框输入：`/sr`
   - 仅报告本次改动新增、可明确复现的安全问题（<0.8 置信度不报告）。

5) 修复 → 复跑 2-4 → 提交 PR
   - `git add -A && git commit -m "feat: 完成功能 X 并通过本地审查" && git push`
   - 可选：`gh pr create -f`
   - 若已接入 GitHub Actions，会在 PR 下自动跑审查。

## 二、快捷命令（一次配置，长期复用）
- 设计审查快捷命令 `/dr`：复制 `design-review/quick-slash-commands.md`（DR-QUICK）到 IDE 的自定义命令。
- 代码审查快捷命令 `/cr`：复制 `code-review/quick-slash-commands.md`（CR-QUICK）。
- 安全审查快捷命令 `/sr`：复制 `security-review/quick-slash-commands.md`（SR-QUICK）。
- 平时只需输入短指令：`/dr …`、`/cr`、`/sr`。

## 三、常见问题最短指引
- 打开空白页：优先用 `http://127.0.0.1`；navigate 后先 `wait_for` 再截图；若失败，收集 console/network/snapshot 以定位。
- GLM 替代 Claude：参考根目录 `USAGE.zh-CN.md` “附录：GLM 脚本式工作流模板”，使用自定义脚本调用 GLM API 并评论到 PR。

## 四、延伸阅读（按需查看）
- 设计审查方法与证据规范：`design-review/design-review-agent.md`
- 设计快捷命令模板：`design-review/quick-slash-commands.md`
- 代码审查快捷命令模板：`code-review/quick-slash-commands.md`
- 安全审查快捷命令模板：`security-review/quick-slash-commands.md`
- GitHub Actions 与 GLM 工作流：`USAGE.zh-CN.md`

（本页仅保留最小可执行信息，避免与上述文档重复。）


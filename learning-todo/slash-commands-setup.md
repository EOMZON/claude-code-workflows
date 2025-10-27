# 斜杠命令配置教程（/dr、/cr、/sr）

目标：一次配置，长期复用。在 IDE（Claude Code 或 GLM 插件）里把长提示固化为快捷命令，后续只输入短指令即可触发完整流程。

## 前置要求
- 已安装并登录 IDE 的 AI 插件（Claude Code 或 GLM 插件）。
- 设计审查需启用 Playwright MCP（否则浏览器相关工具不可用）。
- 本仓库已包含三份快捷模板：
  - 设计：`design-review/quick-slash-commands.md`（DR-QUICK）
  - 代码：`code-review/quick-slash-commands.md`（CR-QUICK）
  - 安全：`security-review/quick-slash-commands.md`（SR-QUICK）

## 一、在 Claude Code 中配置快捷命令
1) 启动claude输入以下指令或者直接复制command文件指令到.claude/commands/配置中
  ```
  > 我需要自定义这些命令，相关文件在docs/workflow  新建命令，命名 `/dr`，将 
  `design-review/quick-slash-commands.md` 的全部内容（DR-QUICK）粘贴进去并保存。
  新建命令，命名 `/cr`，粘贴 `code-review/quick-slash-commands.md`（CR-QUICK）。
   新建命令，命名 `/sr`，粘贴 `security-review/quick-slash-commands.md`（SR-QUICK）。
  ```
2) 启用 Playwright MCP（仅设计审查需要）：
   - 前置安装（本机一次性）：
     - 确认 Node.js ≥ 18：`node -v`
     - 安装浏览器依赖：`npx playwright install --with-deps`
   - 启动方式 A（推荐：由 IDE 启动“命令型 MCP 服务器”）
     - 在 IDE 的 Tools/MCP → Add Server：
       - Name：Playwright MCP
       - Launch Type：Command/Process
       - Command：`npx`
       - Args：`-y mcp-server-playwright --host 127.0.0.1 --port 8800 --headless --viewport-size 1440x900 --allowed-hosts *`
         - 如需联外访问（例如调用你站外 API），可加：`--allowed-origins *`
       - 保存后连接；连接成功即会在工具列表看到 `mcp__playwright__browser_*`
   - 启动方式 B（调试：手动先起再用 IDE 连接 SSE）
     - 终端运行：
       ```bash
       npx -y mcp-server-playwright \
         --host 127.0.0.1 \
         --port 8800 \
         --headless \
         --viewport-size 1440x900 \
         --allowed-hosts *
       ```
     - 在 IDE 的 Tools/MCP → Add Server：
       - Launch Type：HTTP/SSE Endpoint
       - URL：`http://127.0.0.1:8800`
       - 保存并连接
   - 验证：
     - 在对话中运行 `/dr http://127.0.0.1:3000/`
     - 应可调用以下工具并产出证据：
       `mcp__playwright__browser_install / _navigate / _wait_for / _take_screenshot / _console_messages / _network_requests / _snapshot`
   - 常见问题：
     - 空白页：确保本地 URL 可达；navigate 后务必 `browser_wait_for` 再截图；必要时把主机名改为 `127.0.0.1`。
     - 访问受限：为跨域或外部资源访问需要加 `--allowed-origins *`；仅本机服务可省略。
     - 浏览器未安装：执行 `npx playwright install --with-deps` 后重试。

使用方式：
- 设计审查：`/dr http://127.0.0.1:3000/ http://127.0.0.1:3000/feature-x`
- 代码审查：`/cr`
- 安全审查：`/sr`

## 二、在 GLM 插件中配置（若你用 GLM 4.6）
1) 打开插件的“自定义命令/工作流”。
2) 同样新建 `/dr`、`/cr`、`/sr` 三个命令，并分别粘贴对应的 QUICK 模板内容。
3) 若插件支持 MCP：启用并连接 Playwright MCP；若不支持，则保留 `/cr`、`/sr`，`/dr` 只能执行非浏览器步骤或临时跳过。

## 三、验证配置是否成功
- 本地服务启动并可达：`curl -I http://127.0.0.1:3000`（替换为你的端口）。
- 在 IDE 对话框输入：
  - `/dr http://127.0.0.1:3000/` → 期待产出截图、DOM 片段、console/network 摘要与结构化报告；
  - `/cr` → 期待产出 Summary / Critical / Improvements / Nits；
  - `/sr` → 期待产出带文件+行号的安全报告。
- 若提示“未知命令”，说明命令未保存成功；返回命令列表确认。

## 四、常见问题速查
- 浏览器工具不可用：Playwright MCP 未连接或未安装浏览器依赖；按设计审查文档完成安装与连接。
- 打开空白页：改用 `http://127.0.0.1`；在截图前使用 `browser_wait_for` 等待 `domcontentloaded` 和关键选择器；收集 console/network/snapshot 排查。
- 命令执行但无内容：检查本地服务是否启动、URL 是否正确、IDE 的网络/工具权限设置。

## 五、延伸参考
- 快速开始与最小执行清单：`learning-todo/README.md`
- GLM 脚本式工作流与 PR 自动化：`USAGE.zh-CN.md`
- 设计审查方法与输出结构：`design-review/design-review-agent.md`

配置完成后，日常只需输入 `/dr …`、`/cr`、`/sr` 即可，无需再粘贴长提示。

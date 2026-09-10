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

## 六、故事：Todo 团队从立项到上线，用哪些命令/提示

以下用一个「学习版 Todo 应用」的新功能为线索，串起整个开发流程中“在哪个节点用什么命令/提示词”。功能设定：给任务列表新增「标签筛选 + 批量完成」能力，并优化列表项视觉层级。

1) 立项/需求澄清（未写代码）
   - 目标：把需求拆成可验证的交互与设计验收点。
   - 准备：把 `design-review/design-principles-example.md` 复制为 `context/design-principles.md`；新建 `context/style-guide.md` 存放团队品牌与组件规范；把 `design-review/design-review-claude-md-snippet.md` 追加到项目 `CLAUDE.md` 便于后续自检。
   - 提示词（自然语言，对话粘贴即可）：
     - 「参考 `context/design-principles.md` 与 `context/style-guide.md`，帮我把‘标签筛选+批量完成’拆成交互流程与可访问性验收点，按 Blocker/High/Medium/Nit 分级。」
     - 「基于原则，建议列表项信息层级与组件选型（下拉/多选/Chip），并给出移动端折叠策略。」

2) 设计草稿/技术方案评审（开始写样式/组件前）
   - 目标：在动手前先做一次“纸上”评审，避免返工。
   - 提示词：
     - 「请用 `context/design-principles.md` 逐条审视这份交互草图/技术方案，指出可能的视觉一致性与可用性风险，并给出‘更稳妥默认值’建议。」
   - 补充：若你已经在 `CLAUDE.md` 中加入了快速自检清单（见 `design-review/design-review-claude-md-snippet.md`），可直接对照执行。

3) 本地开发中（第一次能跑起来时）
   - 目标：最小可用版本跑通后，立刻做“证据驱动”的轻量设计检查。
   - 适用命令：
     - 设计快速检查（URL 直连）：`/dr http://127.0.0.1:3000/ http://127.0.0.1:3000/tasks`
       - 说明：`/dr` 源自 `design-review/quick-slash-commands.md`（DR-QUICK），会自动截图、抓取 console/network 与 DOM 片段；若是 SPA，记得等待根节点选择器。
     - 可选：再次运行 `/dr` 并在对话中补充「请分别在 1440/768/375 视口下截图对比并标注布局问题」。
   - 提示词（若需额外分析）：
     - 「基于截图证据，指出列表项的对齐、间距、对比度是否满足 `context/design-principles.md`。」

4) 开发完成，准备提 PR（合并前本地全量审查）
   - 目标：一次覆盖“代码质量 + 安全 + 完整设计审查”。
   - 适用命令：
     - 代码审查：`/cr`（来源 `code-review/quick-slash-commands.md`）
     - 安全审查：`/sr`（来源 `security-review/quick-slash-commands.md`）
     - 设计差异审查（基于 git diff 的正式版本）：配置并运行 `/design-review`（内容见 `design-review/design-review-slash-command.md`）
       - 提示：确保存在 `context/design-principles.md` 与 `context/style-guide.md`，否则报告会缺少对标依据。

5) 评审打回与修复（迭代中）
   - 目标：面向证据逐条修复 Blocker/High 项；每修一类问题就局部复跑。
   - 适用命令：
     - 设计快速复查：`/dr` 仅对受影响 URL 复跑，确认问题消除。
     - 代码/安全：视改动范围决定是否复跑 `/cr`、`/sr`。
   - 提示词：
     - 「针对报告中的 [Blocker] ‘复选框焦点可见性不足’，给出最小改动的修复建议（引用文件与行号），并说明为何满足 WCAG AA。」

6) PR 合并前最后一跳（预览环境/Staging）
   - 目标：在和生产更接近的环境再跑一次 URL 级别检查，兜底资源/配置差异。
   - 适用命令：
     - 设计检查：`/dr https://staging.example.com/ https://staging.example.com/tasks`
   - 提示词：
     - 「对比本地与 Staging 的截图，标注字体/颜色/阴影差异，并判断是否由 CSS 构建或环境变量导致。」

7) 上线后健康检查与回归
   - 目标：验证关键路径仍然良好，并记录证据。
   - 适用命令：
     - 设计检查（线上）：`/dr https://app.example.com/ https://app.example.com/tasks`
   - 提示词：
     - 「基于线上截图与 console/network 摘要，评估首屏可感知性能与交互就绪时机，提出 1-2 条高性价比优化建议。」

小结：
- URL 级快速检查 → 用 `/dr`（DR-QUICK）。
- 基于 git diff 的正式设计评审 → 用 `/design-review`（需要提前把 `design-review/design-review-slash-command.md` 注册为命令）。
- 代码质量与安全 → `/cr`、`/sr` 搭配运行。
- 全流程都以 `context/design-principles.md` 与 `context/style-guide.md` 为依据，`CLAUDE.md` 中的自检清单负责“随写随查”。

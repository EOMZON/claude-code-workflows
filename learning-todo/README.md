# 功能完成后的本地审查最佳实践（含提示词模板）

面向本地开发者：当你完成一段功能后，按本文的顺序快速做一次“设计 + 代码 + 安全”三合一审查，尽量用工具产物作为证据，避免主观臆断与模型幻觉。适用于 Claude Code 或替代插件（如 GLM 4.6）。

## 一、前置准备
- 本地服务可访问（建议 `http://127.0.0.1:PORT`）。
- 已配置并可调用 Playwright MCP（浏览器安装成功）。
- IDE 已配置好斜杠命令或子代理：`/design-review`、`/review`、`/security-review`（或同等命令）。
- 若使用 GLM：已在插件内配置 `GLM_API_KEY` 与模型 ID（如 `glm-4.6`）。

## 二、最佳实践执行顺序
1) 基础自检
   - 运行单测、类型检查、Lint/格式化（尽可能清零）。
   - 启动本地服务，手工冒烟走一遍关键流程。

2) 设计审查（Playwright MCP）
   - 先安装浏览器依赖：`mcp__playwright__browser_install`
   - 访问页面：`mcp__playwright__browser_navigate`
   - 等待就绪：`mcp__playwright__browser_wait_for`（`domcontentloaded` 或关键选择器）
   - 收集证据：截图、DOM 片段、Console/Network 概要

3) 代码审查（本地即时）
   - 基于最近提交差异或工作区改动，让代理给出架构/正确性/可维护/测试/性能/依赖等维度建议。

4) 安全审查（本地即时）
   - 用高置信度过滤，仅报告具备清晰攻击路径的新增安全问题。

5) 迭代修复 → 再次运行 2-4 步 → 提交 PR
   - 推送后，GitHub Actions 会在 PR 上自动审查（若已接入自动化）。

## 三、反幻觉与证据要求（强烈建议）
- 先跑工具、再下结论；结论要附“证据 ID”。
- 每条设计发现至少包含：1 张截图 + 关键 DOM 选择器/片段 + Console/Network 摘要。
- 页面不可达或工具失败时，输出失败原因与复现步骤，禁止编造页面结构。

## 四、可复制的提示词模板（按需精简）

### 1) 设计审查（带 Playwright MCP）
用于 `/design-review` 或等效命令。建议粘贴到命令配置中。

```
你是高级设计审查专家。请对本地功能进行“证据优先”的设计审查，严格遵循以下流程：

目标 URL 列表（逐个审）：
- http://127.0.0.1:PORT/pathA
- http://127.0.0.1:PORT/pathB

[加载与证据收集]
1. mcp__playwright__browser_install
2. 对每个 URL：
   - mcp__playwright__browser_navigate(url)
   - mcp__playwright__browser_wait_for("domcontentloaded")；若是 SPA，再等待关键选择器（如 #root 或 [data-testid="app-ready"]，若不存在请换等价选择器）
   - mcp__playwright__browser_take_screenshot(fullPage=true)
   - mcp__playwright__browser_console_messages（仅保留 error/warn 摘要）
   - mcp__playwright__browser_network_requests（主文档与关键资源的状态/时序摘要）
   - mcp__playwright__browser_snapshot（截取关键 DOM 片段，避免过大输出）

[评审维度]
- 交互/流程：关键路径是否通顺，破坏性操作是否有二次确认
- 响应式：1440/768/375 视口检查（可通过 browser_resize 重复截图）
- 视觉打磨：对齐/间距/层级/排版/配色一致性
- 可访问性：键盘可达、焦点可见、语义化、对比度、表单标签/Alt 文本
- 稳健性：加载/空/错误/溢出状态

[反幻觉约束]
- 禁止凭常识想象 UI。所有结论必须绑定具体证据（截图/DOM/console/network），否则标记为“证据不足”。
- 页面不可达或工具失败时，报告原因与复现步骤。

[输出结构]
### Design Review Summary
（正向评价 + 总体结论）

### Findings
- [Blocker/High/Medium/Nit] 发现标题（evidence: screenshot#n, dom#n, log#n）
  - 影响与理由（可引用设计原则/可访问性标准）
  - 涉及视口：Desktop/Tablet/Mobile（如适用）

### Evidence
- screenshot#n：（简述）
- dom#n：（关键片段或选择器）
- log#n：（console/network 摘要）

### Limitations / Next Steps
（当前局限与下一步验证建议）
```

提示：若经常出现空白页面，先改用 `http://127.0.0.1`，并在 navigate 前轮询端口存活，通过 `browser_wait_for` 等待关键选择器再截图。

### 2) 代码审查（务实质量）
用于 `/review` 或等效命令。

```
基于“务实质量”框架审查以下改动（建议自动收集 git diff 或直接读取工作区变更）：

[审查重点]
- 架构与完整性：原子性、模块化、抽象与边界
- 功能与正确性：边界/错误/异常输入处理，状态流与幂等
- 安全：输入校验/认证授权/敏感信息/加密/日志泄露
- 可维护性：命名、可读性、控制流、重复/抽象、错误信息
- 测试策略：覆盖率与失败路径、可维护性与隔离、集成/E2E 缺口
- 性能与可扩展性：N+1、索引、算法、缓存、前端体积与渲染
- 依赖与文档：必要性、安全性、维护状态、许可证，文档同步

[输出结构]
### Code Review Summary
（总体评估与关键风险）

### Critical Issues（必须在合并前修复）
- 文件:行号：问题 + 工程原则依据 + 修复思路

### Suggested Improvements
- 文件:行号：建议 + 理由

### Nits
- Nit: 文件:行号：小建议

[风格]
- 关注“净正收益”，避免为小问题阻塞；建议具体、可执行，并说明“为什么”。
```

### 3) 安全审查（高置信度过滤）
用于 `/security-review` 或等效命令。

```
请仅审查本次新增改动的安全影响（忽略既有问题），并以高置信度过滤：只有在可明确给出攻击路径/可利用条件时才报告。

[范围提示]
- 输入验证：SQL/NoSQL 注入、模板/命令/XML/路径注入
- 认证授权：绕过、越权、会话/JWT 问题
- 加密与密钥：硬编码、弱算法、密钥存储、随机性、证书校验
- 注入与执行：反序列化、eval 注入、XSS（仅确认可利用）
- 数据暴露：敏感日志/PII/API 泄露/调试信息外泄

[排除项（误报过滤）]
- 性能/资源问题、节流/配额、文档问题、客户端权限缺失等非漏洞项

[输出结构（Markdown）]
# Vuln N: <类别> `<文件:行号>`
* Severity: High/Medium/Low
* Description: 说明问题与触发条件
* Exploit Scenario: 具体攻击路径与可复现步骤
* Recommendation: 修复建议
* Confidence: 0.8-1.0（<0.8 不要上报）
```

## 五、PR 阶段的自动化
- 使用本仓库的 GitHub Actions 模板：
  - 代码审查：`code-review/claude-code-review.yml`（或自定义版）
  - 安全审查：`security-review/security.yml`
- 若你使用 GLM 替代 Claude，请参考 `USAGE.zh-CN.md` 附录的“GLM 脚本式工作流模板”，改为自定义脚本调用 GLM 接口并评论到 PR。

## 六、常见问题
- 打开空白页：
  - 确保本地服务可达（`127.0.0.1` 优先于 `localhost`）；
  - navigate 后增加 `browser_wait_for` 等待关键选择器；
  - 收集 console/network 快照定位错误与 404/503；
  - Dev HMR 失败可临时关闭或修正 WS 地址。
- 证据太大：
  - 截图保留 1440×900 与移动端一张；
  - DOM 仅截取关键节点；
  - Console/Network 提供摘要与代表性条目链接。

---
如需，我可以把以上模板直接写入你的斜杠命令与子代理配置，或为 GLM 版本生成对应的预设命令文件。


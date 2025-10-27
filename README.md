# Claude Code Workflows（Claude 代码工作流）
The best workflows and configurations I've developed heavily using Claude Code since the day of it's release. Workflows are based off applied learnings from our AI-native startup.  
自从 Claude Code 发布以来，我持续深入使用并沉淀出这些最佳工作流与配置，所有流程都源自我们 AI 原生创业团队的实战经验。

Workflows are covered in detail with tutorials and demos on [Patrick Ellis' YouTube channel](https://www.youtube.com/@PatrickOakleyEllis).  
您可以在 [Patrick Ellis 的 YouTube 频道](https://www.youtube.com/@PatrickOakleyEllis) 中找到涵盖这些工作流的详细教程与演示。

## Workflows（工作流概览）

### [Code Review Workflow](./code-review/)（代码审查工作流）
An automated code review system inspired by Anthropic's own Claude Code development process, where AI agents handle the "blocking and tackling" of code review. This workflow implements dual-loop architecture with slash commands and GitHub Actions to automatically review PRs for syntax, completeness, style guide adherence, and bug detection. Free your team to focus on strategic thinking and architectural alignment while AI handles routine checks. [Watch the tutorial](https://www.youtube.com/watch?v=nItsfXwujjg).  
该自动化代码审查系统源自 Anthropic 构建 Claude Code 时的实践经验，由 AI 代理负责代码审查中的重复性工作。它采用双循环架构，结合斜杠命令与 GitHub Actions，对拉取请求进行语法、完整性、风格规范和缺陷检测的自动检查，让团队能够专注于战略性思考与架构一致性。[观看教程](https://www.youtube.com/watch?v=nItsfXwujjg)。

### [Security Review Workflow](./security-review/)（安全审查工作流）
An automated security review system that proactively identifies vulnerabilities, exposed secrets, and potential attack vectors in your codebase. Based on Anthropic's security-focused approach and OWASP Top 10 standards, this workflow provides severity-classified findings with clear remediation guidance. Includes slash commands for on-demand scanning and GitHub Actions for automated PR security checks. [Watch the tutorial](https://www.youtube.com/watch?v=nItsfXwujjg).  
该自动化安全审查系统可主动识别代码库中的漏洞、泄露的密钥以及潜在攻击向量。它基于 Anthropic 的安全实践与 OWASP Top 10 标准，对安全问题进行分级并给出明确的修复建议，同时支持斜杠命令即时扫描与 GitHub Actions 持续监测。[观看教程](https://www.youtube.com/watch?v=nItsfXwujjg)。

### [Design Review Workflow](./design-review/)（设计审查工作流）
An automated design review system that provides comprehensive feedback on front-end code changes. This workflow uses Microsoft's open source [Playwright MCP](https://github.com/microsoft/playwright-mcp) browser automation and specialized Claude Code agents to ensure UI/UX consistency, accessibility compliance, and adherence to world-class design standards. Perfect for maintaining design quality across teams and catching visual issues before they reach production. [Watch the tutorial](https://www.youtube.com/watch?v=xOO8Wt_i72s).  
该自动化设计审查系统为前端代码变更提供全面反馈，借助微软开源的 [Playwright MCP](https://github.com/microsoft/playwright-mcp) 浏览器自动化以及定制的 Claude Code 代理，确保 UI/UX 一致性、可访问性合规以及对标一流设计标准，非常适合跨团队保持设计质量并在上线前捕获视觉问题。[观看教程](https://www.youtube.com/watch?v=xOO8Wt_i72s)。

---

*More workflows coming soon...*  
*更多工作流即将推出，敬请期待……*

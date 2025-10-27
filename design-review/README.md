# Design Review Workflow（设计审查工作流）

This directory contains templates and examples for implementing an automated design review system that provides feedback on front-end code changes with design implications. This workflow allows engineers to automatically run design reviews on pull requests or working changes, ensuring design consistency and quality throughout the development process.  
本目录提供构建自动化设计审查系统的模板与示例，用于对具有设计影响的前端代码变更提供反馈。该工作流让工程师可以在拉取请求或本地改动上自动执行设计审查，从而在整个开发过程中保持设计一致性与高质量。

## Concept（核心概念）

This workflow establishes a comprehensive methodology for automated design reviews in Claude Code, leveraging multiple advanced features to ensure world-class UI/UX standards in your codebase:  
此工作流在 Claude Code 中建立了一套完整的自动化设计审查方法论，结合多项高级特性，确保代码库达到世界级的 UI/UX 标准：

**Core Methodology | 核心方法论：**
- **Automated Design Reviews | 自动化设计审查**：Trigger comprehensive design assessments either automatically on PRs or on-demand via slash commands  
  通过自动触发或斜杠命令按需启动全面的设计评估。
- **Live Environment Testing | 实时环境测试**：Uses [Playwright MCP](https://github.com/microsoft/playwright-mcp) server integration to interact with and test actual UI components in real-time, not just static code analysis  
  集成 [Playwright MCP](https://github.com/microsoft/playwright-mcp) 服务器，与真实 UI 组件实时交互和测试，而不仅限于静态代码分析。
- **Standards-Based Evaluation | 基于标准的评估**：Follows rigorous design principles inspired by top-tier companies (Stripe, Airbnb, Linear), covering visual hierarchy, accessibility (WCAG AA+), responsive design, and interaction patterns  
  借鉴顶尖公司（Stripe、Airbnb、Linear）的严格设计原则，涵盖视觉层次、可访问性（WCAG AA+）、响应式设计与交互模式。

**Implementation Features | 实践特性：**
- **Claude Code Subagents | Claude Code 子代理**：Deploy specialized design review agents with pre-configured tools and prompts for consistent, thorough reviews, by tagging `@agent-code-reviewer`  
  通过标记 `@agent-code-reviewer` 部署预先配置工具和提示的专业设计审查代理，提供一致且深入的评估。
- **Slash Commands | 斜杠命令**：Enable instant design reviews with `/design-review` that automatically analyzes git diffs and provides structured feedback  
  使用 `/design-review` 即刻触发设计审查，自动分析 git 差异并输出结构化反馈。
- **CLAUDE.md Memory Integration | CLAUDE.md 记忆集成**：Store design principles and brand guidelines in your project's CLAUDE.md file, ensuring Claude Code always references your specific design system  
  将设计原则与品牌指南存储在项目的 CLAUDE.md 中，确保 Claude Code 始终引用你的专属设计体系。
- **Multi-Phase Review Process | 多阶段审查流程**：Systematic evaluation covering interaction flows, responsiveness, visual polish, accessibility, robustness testing, and code health  
  通过多阶段流程系统评估交互流程、响应性、视觉打磨、可访问性、稳健性测试以及代码健康度。

This approach transforms design reviews from manual, subjective processes into automated, objective assessments that maintain consistency across your entire frontend development workflow.  
该方法将设计审查从手工、主观的流程转变为自动化、客观的评估，确保整个前端开发流程保持一致性。

## Resources（资源）

### Templates & Examples（模板与示例）
- [Design Principles Example](./design-principles-example.md) - Sample design principles document for guiding automated reviews  
  [Design Principles Example](./design-principles-example.md) —— 用于指导自动化审查的设计原则示例文档。
- [Design Review Agent](./design-review-agent.md) - Agent configuration for automated design reviews  
  [Design Review Agent](./design-review-agent.md) —— 自动化设计审查的代理配置。
- [Claude.md Snippet](./design-review-claude-md-snippet.md) - Claude.md configuration snippet for design review integration  
  [Claude.md Snippet](./design-review-claude-md-snippet.md) —— 集成设计审查的 CLAUDE.md 配置片段。
- [Slash Command](./design-review-slash-command.md) - Custom slash command implementation for on-demand design reviews  
  [Slash Command](./design-review-slash-command.md) —— 支持按需设计审查的自定义斜杠命令实现。

### Video Tutorial（视频教程）
For a detailed walkthrough of this workflow, watch the comprehensive tutorial on YouTube: [Patrick Ellis' Channel](https://www.youtube.com/watch?v=xOO8Wt_i72s)  
若需了解该工作流的详细操作，请观看 YouTube 上的完整教程：[Patrick Ellis 频道](https://www.youtube.com/watch?v=xOO8Wt_i72s)。

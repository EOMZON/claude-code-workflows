# Code Review Workflow（代码审查工作流）

This directory contains templates and examples for implementing an automated code review system that provides comprehensive feedback on code changes. This workflow, inspired by Anthropic's own Claude Code development process and their [claude-code-action](https://github.com/anthropics/claude-code-action) GitHub repository, enables teams to scale code review capacity while maintaining high quality standards through AI-assisted reviews.  
本目录包含用于构建自动化代码审查系统的模板与示例，该系统能为代码变更提供全面反馈。工作流灵感来自 Anthropic 在 Claude Code 项目中的实践以及其 [claude-code-action](https://github.com/anthropics/claude-code-action) GitHub 仓库，帮助团队在 AI 辅助的支持下扩展代码审查能力，同时保持高标准的质量要求。

## Concept（核心概念）

This workflow establishes a comprehensive methodology for automated code reviews in Claude Code, replacing manual line-by-line reviews with intelligent AI agents that handle pattern matching and consistency checks:  
此工作流为 Claude Code 中的自动化代码审查建立了一套完整的方法论，用智能 AI 代理替代手动逐行审查，负责模式匹配与一致性检查：

**Core Methodology | 核心方法论：**
- **Automated Code Reviews | 自动化代码审查**：Deploy AI reviewers that handle the "blocking and tackling" of code review - syntax, completeness, style guide adherence, and bug detection  
  部署 AI 审查员负责代码审查中的基础性工作，例如语法检查、完整性验证、风格指南遵循与缺陷检测。
- **Dual-Loop Architecture | 双循环架构**：Leverage both inner loop (slash commands, subagents) for iterative development and outer loop (GitHub Actions) for automated PR validation  
  通过内循环（斜杠命令、子代理）支持迭代开发，通过外循环（GitHub Actions）自动验证拉取请求。
- **Standards-Based Evaluation | 标准驱动评估**：Enforce consistent code quality through pattern matching, fast analysis, and adherence to your team's specific coding standards  
  通过模式匹配与快速分析确保代码质量一致，并遵循团队定制的编码标准。
- **Human-AI Collaboration | 人机协同**：Free human reviewers to focus on high-level strategic thinking, architectural alignment, and business logic while AI handles routine checks  
  让人类审查者专注于战略性思考、架构一致性与业务逻辑，常规检查交由 AI 处理。

**Implementation Features | 落地特性：**
- **Claude Code Subagents | Claude Code 子代理**：Deploy specialized code review agents that preserve context and provide detailed analysis without consuming main thread tokens  
  部署专门的代码审查代理，在不消耗主线程 Tokens 的情况下保留上下文并提供详尽分析。
- **Slash Commands | 斜杠命令**：Enable instant code reviews with `/review` that automatically analyzes recent commits or specified PRs  
  通过 `/review` 命令即时触发代码审查，自动分析最近提交或指定的拉取请求。
- **GitHub Actions Integration | GitHub Actions 集成**：Fully automated reviewers that run on every PR, providing consistent feedback before human review  
  在每个 PR 上运行的全自动审查流程，在人工审查之前就提供一致的反馈。
- **Customizable Review Criteria | 可定制审查标准**：Tailor review standards to your organization's specific needs, architectural patterns, and coding conventions  
  可根据组织的特定需求、架构模式与编码约定自定义审查标准。
- **Learning Opportunities | 学习机会**：Teams learn from AI-generated reviews, improving their understanding of best practices and common pitfalls  
  团队可以从 AI 生成的审查中学习，深化对最佳实践与常见陷阱的理解。

This approach, battle-tested by Anthropic's own engineering team building Claude Code with Claude Code, enables teams to handle the increased volume of AI-generated code while maintaining rigorous quality standards.  
Anthropic 工程团队在使用 Claude Code 构建 Claude Code 的过程中验证了该方案，帮助团队在应对海量 AI 生成代码时仍能保持严格的质量标准。

## Resources（资源）

### Templates & Examples（模板与示例）
- [Claude Code Review YAML](./claude-code-review.yml) - Standard GitHub Action configuration for automated code reviews  
  [Claude Code Review YAML](./claude-code-review.yml) —— 用于自动化代码审查的标准 GitHub Action 配置。
- [Custom Code Review YAML](./claude-code-review-custom.yml) - Extended configuration with custom review criteria  
  [Custom Code Review YAML](./claude-code-review-custom.yml) —— 扩展配置，支持自定义审查标准。
- [Pragmatic Code Review Slash Command](./pragmatic-code-review-slash-command.md) - Custom slash command for on-demand pragmatic code reviews  
  [Pragmatic Code Review Slash Command](./pragmatic-code-review-slash-command.md) —— 自定义斜杠命令，可按需触发务实型代码审查。
- [Pragmatic Code Review Subagent](./pragmatic-code-review-subagent.md) - Subagent configuration for comprehensive code analysis  
  [Pragmatic Code Review Subagent](./pragmatic-code-review-subagent.md) —— 子代理配置，支持全面的代码分析。

### Video Tutorial（视频教程）
For a detailed walkthrough of this workflow, watch the [comprehensive tutorial on YouTube](https://www.youtube.com/watch?v=nItsfXwujjg).  
想了解详细的操作演示，请观看这份 [YouTube 上的完整教程](https://www.youtube.com/watch?v=nItsfXwujjg)。

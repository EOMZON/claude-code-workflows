# Security Review Workflow（安全审查工作流）

This directory contains templates and examples for implementing an automated security review system that provides comprehensive vulnerability scanning and security analysis on code changes. This workflow is inspired by and taken from Anthropic's [claude-code-security-review](https://github.com/anthropics/claude-code-security-review) GitHub repository, enabling teams to proactively identify and address security issues before they reach production.  
本目录提供用于构建自动化安全审查系统的模板与示例，该系统对代码变更执行全面的漏洞扫描与安全分析。工作流借鉴并来源于 Anthropic 的 [claude-code-security-review](https://github.com/anthropics/claude-code-security-review) GitHub 仓库，帮助团队在问题进入生产环境之前主动发现并修复安全隐患。

## Concept（核心概念）

This workflow establishes a comprehensive methodology for automated security reviews in Claude Code, leveraging AI agents to detect vulnerabilities and enforce security best practices:  
此工作流在 Claude Code 中建立了一套完整的自动化安全审查方法论，利用 AI 代理检测漏洞并执行安全最佳实践：

**Core Methodology | 核心方法论：**
- **Automated Security Scanning | 自动化安全扫描**：Deploy AI-powered security reviewers that identify vulnerabilities, exposed secrets, and potential attack vectors  
  部署 AI 驱动的安全审查员，识别漏洞、泄露的密钥与潜在攻击向量。
- **OWASP-Based Analysis | 基于 OWASP 的分析**：Follow industry-standard security frameworks including OWASP Top 10 to ensure comprehensive coverage  
  遵循包括 OWASP Top 10 在内的行业标准安全框架，确保覆盖全面。
- **Severity Classification | 严重程度分类**：Automatically categorize findings by severity level (Critical, High, Medium, Low) with clear remediation guidance  
  自动按严重程度（致命、高、中、低）对发现的问题进行分类，并提供明确的修复指导。
- **False Positive Management | 误报管理**：Intelligent filtering to reduce noise and focus on real security issues  
  通过智能过滤降低噪声，聚焦真实的安全问题。

**Implementation Features | 落地特性：**
- **Slash Commands | 斜杠命令**：Enable instant security reviews with `/security-review` that analyzes recent changes for security vulnerabilities  
  使用 `/security-review` 即刻触发安全审查，分析近期改动中的安全漏洞。
- **GitHub Actions Integration | GitHub Actions 集成**：Automated security scanning on every PR, with inline comments highlighting specific security concerns  
  在每个 PR 上自动执行安全扫描，并通过行内评论标注具体安全问题。
- **Secret Detection | 密钥检测**：Identify exposed API keys, credentials, and sensitive information before they're committed  
  在提交前识别暴露的 API 密钥、凭据及敏感信息。
- **Dependency Analysis | 依赖分析**：Review third-party dependencies for known vulnerabilities and security risks  
  审查第三方依赖，识别已知漏洞和安全风险。
- **Custom Security Policies | 自定义安全策略**：Configure organization-specific security requirements and compliance standards  
  配置组织特有的安全要求与合规标准。

This approach ensures that security is built into the development process from the start, catching vulnerabilities early when they're easiest and least expensive to fix.  
该方案确保从开发早期就嵌入安全保障，在最容易且成本最低的阶段捕获漏洞。

## Resources（资源）

### Templates & Examples（模板与示例）
- [Security Review Slash Command](./security-review-slash-command.md) - Default security review command from Anthropic (source: [claude-code-security-review](https://github.com/anthropics/claude-code-security-review))  
  [Security Review Slash Command](./security-review-slash-command.md) —— 来自 Anthropic 的默认安全审查命令（参考来源：[claude-code-security-review](https://github.com/anthropics/claude-code-security-review)）。
- [Security YAML](./security.yml) - GitHub Action configuration for automated security scanning  
  [Security YAML](./security.yml) —— 自动化安全扫描的 GitHub Action 配置。

### Video Tutorial（视频教程）
For a detailed walkthrough of this workflow, watch the [comprehensive tutorial on YouTube](https://www.youtube.com/watch?v=nItsfXwujjg).  
如需详细了解该工作流，请观看 [YouTube 上的完整教程](https://www.youtube.com/watch?v=nItsfXwujjg)。

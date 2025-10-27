---
name: SR-QUICK
description: Quick security review with high-confidence filtering. Report only exploitable, newly introduced issues.
allowed-tools: Bash(git diff:*), Bash(git status:*), Bash(git log:*), Read, Grep, LS
---

你是资深安全工程师，仅审查本次新增改动的安全影响。严格高置信度过滤（<0.8 不上报）。

收集上下文：
GIT STATUS:
```
!`git status`
```
FILES MODIFIED:
```
!`git diff --name-only origin/HEAD...`
```
COMMITS:
```
!`git log --no-decorate origin/HEAD...`
```
DIFF CONTENT:
```
!`git diff --merge-base origin/HEAD`
```

输出（Markdown，每条漏洞）：文件/行号、Severity、Category、Description、Exploit Scenario、Recommendation、Confidence。
范围示例：输入验证（SQL/NoSQL/模板/命令/XML/路径）、认证授权（绕过/越权/会话/JWT）、加密与密钥（硬编码/弱算法/存储/随机性/证书）、注入与执行（反序列化/eval/XSS）、数据暴露（敏感日志/PII/API/调试信息）。
排除：性能与资源、节流/配额、文档、客户端权限缺失等非漏洞项。


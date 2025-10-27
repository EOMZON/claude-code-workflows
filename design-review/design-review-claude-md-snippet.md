## Visual Development（视觉开发）

### Design Principles（设计原则）
- Comprehensive design checklist in `/context/design-principles.md`  
  详尽的设计检查清单位于 `/context/design-principles.md`
- Brand style guide in `/context/style-guide.md`  
  品牌风格指南位于 `/context/style-guide.md`
- When making visual (front-end, UI/UX) changes, always refer to these files for guidance  
  进行视觉（前端、UI/UX）更改时，请始终参考这些文件获取指导

### Quick Visual Check（快速视觉检查）
IMMEDIATELY after implementing any front-end change:  
在完成任何前端改动后立即执行：
1. **Identify what changed** - Review the modified components/pages  
   **确认变动内容**：检查被修改的组件或页面
2. **Navigate to affected pages** - Use `mcp__playwright__browser_navigate` to visit each changed view  
   **访问受影响页面**：使用 `mcp__playwright__browser_navigate` 查看每个变动视图
3. **Verify design compliance** - Compare against `/context/design-principles.md` and `/context/style-guide.md`  
   **验证设计合规性**：对照 `/context/design-principles.md` 与 `/context/style-guide.md`
4. **Validate feature implementation** - Ensure the change fulfills the user's specific request  
   **确认功能实现**：确保改动满足用户的具体需求
5. **Check acceptance criteria** - Review any provided context files or requirements  
   **检查验收标准**：复核相关上下文文件或需求
6. **Capture evidence** - Take full page screenshot at desktop viewport (1440px) of each changed view  
   **采集证据**：在桌面视口（1440px）下为每个改动页面截取全屏图
7. **Check for errors** - Run `mcp__playwright__browser_console_messages`  
   **检查错误**：运行 `mcp__playwright__browser_console_messages`

This verification ensures changes meet design standards and user requirements.  
上述验证流程可确保改动符合设计标准与用户需求。

### Comprehensive Design Review（全面设计审查）
Invoke the `@agent-design-review` subagent for thorough design validation when:  
在以下情境下调用 `@agent-design-review` 子代理以进行深入设计验证：
- Completing significant UI/UX features  
  完成重要的 UI/UX 功能时
- Before finalizing PRs with visual changes  
  在合并包含视觉改动的 PR 之前
- Needing comprehensive accessibility and responsiveness testing  
  需要全面的可访问性与响应式测试时

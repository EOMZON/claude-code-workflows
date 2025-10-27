# S-Tier SaaS Dashboard Design Checklist (Inspired by Stripe, Airbnb, Linear)（顶级 SaaS 仪表盘设计检查清单）

## I. Core Design Philosophy & Strategy（核心设计理念与策略）

*   [ ] **Users First:** Prioritize user needs, workflows, and ease of use in every design decision.  
        **用户至上：** 在每一次设计决策中都要优先考虑用户需求、工作流程与易用性。
*   [ ] **Meticulous Craft:** Aim for precision, polish, and high quality in every UI element and interaction.  
        **精雕细琢：** 确保每个界面元素与交互都精确、精致且高质量。
*   [ ] **Speed & Performance:** Design for fast load times and snappy, responsive interactions.  
        **速度与性能：** 优化加载速度并提供流畅的响应式交互体验。
*   [ ] **Simplicity & Clarity:** Strive for a clean, uncluttered interface. Ensure labels, instructions, and information are unambiguous.  
        **简洁与清晰：** 保持界面整洁无杂，保证标签、指引与信息表达明确。
*   [ ] **Focus & Efficiency:** Help users achieve their goals quickly and with minimal friction. Minimize unnecessary steps or distractions.  
        **专注与效率：** 帮助用户快速达成目标，减少不必要的步骤与干扰。
*   [ ] **Consistency:** Maintain a uniform design language (colors, typography, components, patterns) across the entire dashboard.  
        **一致性：** 在整个仪表盘中保持颜色、字体、组件与模式的统一设计语言。
*   [ ] **Accessibility (WCAG AA+):** Design for inclusivity. Ensure sufficient color contrast, keyboard navigability, and screen reader compatibility.  
        **可访问性（WCAG AA+）：** 为包容性而设计，确保足够的色彩对比、键盘可操作性与屏幕阅读器兼容性。
*   [ ] **Opinionated Design (Thoughtful Defaults):** Establish clear, efficient default workflows and settings, reducing decision fatigue for users.  
        **有主见的设计（深思熟虑的默认值）：** 建立清晰高效的默认流程与设置，减轻用户决策疲劳。

## II. Design System Foundation (Tokens & Core Components)（设计系统基础：设计令牌与核心组件）

*   [ ] **Define a Color Palette:**  
        **定义调色板：**
    *   [ ] **Primary Brand Color:** User-specified, used strategically.  
            **主品牌色：** 由用户指定并战略性地使用。
    *   [ ] **Neutrals:** A scale of grays (5-7 steps) for text, backgrounds, borders.  
            **中性色：** 为文本、背景和边框定义 5-7 级灰度。
    *   [ ] **Semantic Colors:** Define specific colors for Success (green), Error/Destructive (red), Warning (yellow/amber), Informational (blue).  
            **语义色：** 为成功（绿色）、错误/破坏（红色）、警告（黄色/琥珀色）、信息（蓝色）设定明确色值。
    *   [ ] **Dark Mode Palette:** Create a corresponding accessible dark mode palette.  
            **深色模式调色板：** 创建符合可访问性的深色模式配色。
    *   [ ] **Accessibility Check:** Ensure all color combinations meet WCAG AA contrast ratios.  
            **可访问性检查：** 确保所有颜色组合符合 WCAG AA 对比度要求。
*   [ ] **Establish a Typographic Scale:**  
        **建立排版层级体系：**
    *   [ ] **Primary Font Family:** Choose a clean, legible sans-serif font (e.g., Inter, Manrope, system-ui).  
            **主字体族：** 选择简洁易读的无衬线字体（如 Inter、Manrope、system-ui）。
    *   [ ] **Modular Scale:** Define distinct sizes for H1, H2, H3, H4, Body Large, Body Medium (Default), Body Small/Caption. (e.g., H1: 32px, Body: 14px/16px).  
            **模块化字体比例：** 为 H1、H2、H3、H4、正文大号、正文常规（默认）、正文小号/说明定义明确的字号（例如 H1：32px，正文：14px/16px）。
    *   [ ] **Font Weights:** Utilize a limited set of weights (e.g., Regular, Medium, SemiBold, Bold).  
            **字体粗细：** 使用有限且清晰的字重组合（如 Regular、Medium、SemiBold、Bold）。
    *   [ ] **Line Height:** Ensure generous line height for readability (e.g., 1.5-1.7 for body text).  
            **行高：** 通过较大的行高提升可读性（例如正文行高 1.5-1.7）。
*   [ ] **Define Spacing Units:**  
        **定义间距单位：**
    *   [ ] **Base Unit:** Establish a base unit (e.g., 8px).  
            **基础单位：** 确定一个基础单位（如 8px）。
    *   [ ] **Spacing Scale:** Use multiples of the base unit for all padding, margins, and layout spacing (e.g., 4px, 8px, 12px, 16px, 24px, 32px).  
            **间距刻度：** 所有内外边距与布局间距使用基础单位的倍数（如 4px、8px、12px、16px、24px、32px）。
*   [ ] **Define Border Radii:**  
        **定义圆角半径：**
    *   [ ] **Consistent Values:** Use a small set of consistent border radii (e.g., Small: 4-6px for inputs/buttons; Medium: 8-12px for cards/modals).  
            **一致的取值：** 采用一小组统一的圆角尺寸（如小圆角 4-6px 用于输入/按钮，中圆角 8-12px 用于卡片/模态）。
*   [ ] **Develop Core UI Components (with consistent states: default, hover, active, focus, disabled):**  
        **构建核心 UI 组件（确保默认、悬停、激活、聚焦、禁用等状态一致）：**
    *   [ ] Buttons (primary, secondary, tertiary/ghost, destructive, link-style; with icon options)  
            按钮（主按钮、次按钮、第三级/幽灵按钮、危险按钮、链接样式；支持图标选项）
    *   [ ] Input Fields (text, textarea, select, date picker; with clear labels, placeholders, helper text, error messages)  
            输入字段（文本、文本区、选择器、日期选择器；需包含清晰的标签、占位符、辅助文本与错误信息）
    *   [ ] Checkboxes & Radio Buttons  
            复选框与单选按钮
    *   [ ] Toggles/Switches  
            切换开关
    *   [ ] Cards (for content blocks, multimedia items, dashboard widgets)  
            卡片组件（用于内容块、多媒体项目、仪表盘小部件）
    *   [ ] Tables (for data display; with clear headers, rows, cells; support for sorting, filtering)  
            表格（用于展示数据；需有清晰的表头、行与单元格，并支持排序与筛选）
    *   [ ] Modals/Dialogs (for confirmations, forms, detailed views)  
            模态框/对话框（用于确认、表单、详情视图）
    *   [ ] Navigation Elements (Sidebar, Tabs)  
            导航元素（侧边栏、标签页）
    *   [ ] Badges/Tags (for status indicators, categorization)  
            徽章/标签（用于状态指示与分类）
    *   [ ] Tooltips (for contextual help)  
            工具提示（提供上下文帮助）
    *   [ ] Progress Indicators (Spinners, Progress Bars)  
            进度指示（旋转加载、进度条）
    *   [ ] Icons (use a single, modern, clean icon set; SVG preferred)  
            图标（使用统一、现代、简洁的图标集，推荐 SVG）
    *   [ ] Avatars  
            头像

## III. Layout, Visual Hierarchy & Structure（布局、视觉层次与结构）

*   [ ] **Responsive Grid System:** Design based on a responsive grid (e.g., 12-column) for consistent layout across devices.  
        **响应式栅格系统：** 基于响应式栅格（如 12 栏）设计，以便在不同设备上保持一致布局。
*   [ ] **Strategic White Space:** Use ample negative space to improve clarity, reduce cognitive load, and create visual balance.  
        **策略性留白：** 充分利用负空间提升清晰度、降低认知负荷并营造视觉平衡。
*   [ ] **Clear Visual Hierarchy:** Guide the user's eye using typography (size, weight, color), spacing, and element positioning.  
        **清晰的视觉层次：** 通过字体（大小、粗细、颜色）、间距与元素布局引导用户视线。
*   [ ] **Consistent Alignment:** Maintain consistent alignment of elements.  
        **一致的对齐方式：** 保持界面元素的对齐一致。
*   [ ] **Main Dashboard Layout:**  
        **主仪表盘布局：**
    *   [ ] Persistent Left Sidebar: For primary navigation between modules.  
            固定左侧栏：用于模块之间的主导航。
    *   [ ] Content Area: Main space for module-specific interfaces.  
            内容区域：展示模块特定界面的主要空间。
    *   [ ] (Optional) Top Bar: For global search, user profile, notifications.  
            （可选）顶栏：放置全局搜索、用户信息、通知等。
*   [ ] **Mobile-First Considerations:** Ensure the design adapts gracefully to smaller screens.  
        **移动优先考量：** 确保设计在小屏设备上也能良好呈现。

## IV. Interaction Design & Animations（交互设计与动效）

*   [ ] **Purposeful Micro-interactions:** Use subtle animations and visual feedback for user actions (hovers, clicks, form submissions, status changes).  
        **有目的的微交互：** 使用恰到好处的动画与视觉反馈响应用户操作（悬停、点击、表单提交、状态变化）。
    *   [ ] Feedback should be immediate and clear.  
            反馈需及时且清晰。
    *   [ ] Animations should be quick (150-300ms) and use appropriate easing (e.g., ease-in-out).  
            动画应快速（150-300ms）并采用合适的缓动曲线（如 ease-in-out）。
*   [ ] **Loading States:** Implement clear loading indicators (skeleton screens for page loads, spinners for in-component actions).  
        **加载状态：** 使用清晰的加载指示（页面加载骨架屏、组件内操作的旋转指示等）。
*   [ ] **Transitions:** Use smooth transitions for state changes, modal appearances, and section expansions.  
        **过渡效果：** 在状态变化、模态弹出、版块展开时使用平滑过渡。
*   [ ] **Avoid Distraction:** Animations should enhance usability, not overwhelm or slow down the user.  
        **避免干扰：** 动画应提升可用性，而非造成负担或拖慢体验。
*   [ ] **Keyboard Navigation:** Ensure all interactive elements are keyboard accessible and focus states are clear.  
        **键盘操作：** 确保所有交互元素支持键盘访问并拥有清晰的焦点状态。

## V. Specific Module Design Tactics（特定模块设计策略）

### A. Multimedia Moderation Module（多媒体审核模块）

*   [ ] **Clear Media Display:** Prominent image/video previews (grid or list view).  
        **清晰的媒体展示：** 提供突出的视频/图片预览（网格或列表视图）。
*   [ ] **Obvious Moderation Actions:** Clearly labeled buttons (Approve, Reject, Flag, etc.) with distinct styling (e.g., primary/secondary, color-coding). Use icons for quick recognition.  
        **明确的审核操作：** 使用清晰标签与显著样式（如主次按钮、颜色编码）的按钮（通过、拒绝、标记等），并配合图标提升识别速度。
*   [ ] **Visible Status Indicators:** Use color-coded Badges for content status (Pending, Approved, Rejected).  
        **可见的状态指示：** 使用颜色区分的徽章表示内容状态（待审核、已通过、已拒绝）。
*   [ ] **Contextual Information:** Display relevant metadata (uploader, timestamp, flags) alongside media.  
        **上下文信息：** 在媒体旁显示上传者、时间戳、标记等元数据。
*   [ ] **Workflow Efficiency:**  
        **流程效率：**
    *   [ ] Bulk Actions: Allow selection and moderation of multiple items.  
            批量操作：允许选择并处理多个项目。
    *   [ ] Keyboard Shortcuts: For common moderation actions.  
            键盘快捷键：支持常用审核操作。
*   [ ] **Minimize Fatigue:** Clean, uncluttered interface; consider dark mode option.  
        **减轻疲劳：** 界面简洁，必要时提供深色模式。

### B. Data Tables Module (Contacts, Admin Settings)（数据表格模块：联系人、管理设置）

*   [ ] **Readability & Scannability:**  
        **可读性与可扫描性：**
    *   [ ] Smart Alignment: Left-align text, right-align numbers.  
            智能对齐：文本左对齐、数字右对齐。
    *   [ ] Clear Headers: Bold column headers.  
            清晰表头：使用加粗的列标题。
    *   [ ] Zebra Striping (Optional): For dense tables.  
            斑马条纹（可选）：用于密集数据表。
    *   [ ] Legible Typography: Simple, clean sans-serif fonts.  
            易读字体：选择简洁清晰的无衬线字体。
    *   [ ] Adequate Row Height & Spacing.  
            合理的行高与间距。
*   [ ] **Interactive Controls:**  
        **交互控制：**
    *   [ ] Column Sorting: Clickable headers with sort indicators.  
            列排序：可点击的表头及排序指示。
    *   [ ] Intuitive Filtering: Accessible filter controls (dropdowns, text inputs) above the table.  
            直观筛选：在表格上方提供易用的筛选控件（下拉、文本输入等）。
    *   [ ] Global Table Search.  
            全局表格搜索。
*   [ ] **Large Datasets:**  
        **海量数据处理：**
    *   [ ] Pagination (preferred for admin tables) or virtual/infinite scroll.  
            分页（管理后台推荐）或虚拟/无限滚动。
    *   [ ] Sticky Headers / Frozen Columns: If applicable.  
            粘性表头/冻结列（如适用）。
*   [ ] **Row Interactions:**  
        **行级交互：**
    *   [ ] Expandable Rows: For detailed information.  
            可展开行：展示详情。
    *   [ ] Inline Editing: For quick modifications.  
            行内编辑：便于快速修改。
    *   [ ] Bulk Actions: Checkboxes and contextual toolbar.  
            批量操作：复选框与上下文工具栏。
    *   [ ] Action Icons/Buttons per Row: (Edit, Delete, View Details) clearly distinguishable.  
            行级操作按钮/图标：清晰区分编辑、删除、查看详情等。

### C. Configuration Panels Module (Microsite, Admin Settings)（配置面板模块：微站、管理设置）

*   [ ] **Clarity & Simplicity:** Clear, unambiguous labels for all settings. Concise helper text or tooltips for descriptions. Avoid jargon.  
        **清晰与简单：** 所有设置项需有明确标签，使用精炼的辅助文本或提示解释，避免行话。
*   [ ] **Logical Grouping:** Group related settings into sections or tabs.  
        **逻辑分组：** 将关联设置划分为区块或标签页。
*   [ ] **Progressive Disclosure:** Hide advanced or less-used settings by default (e.g., behind "Advanced Settings" toggle, accordions).  
        **循序展示：** 默认隐藏高级或低频设置（例如使用“高级设置”开关或手风琴）。
*   [ ] **Appropriate Input Types:** Use correct form controls (text fields, checkboxes, toggles, selects, sliders) for each setting.  
        **合适的输入类型：** 为每个设置选择正确的表单控件（文本框、复选框、开关、选择器、滑块等）。
*   [ ] **Visual Feedback:** Immediate confirmation of changes saved (e.g., toast notifications, inline messages). Clear error messages for invalid inputs.  
        **视觉反馈：** 在保存变更时立刻反馈（如 Toast 通知、行内提示），无效输入需提供清晰的错误信息。
*   [ ] **Sensible Defaults:** Provide default values for all settings.  
        **合理默认值：** 所有设置都应提供默认值。
*   [ ] **Reset Option:** Easy way to "Reset to Defaults" for sections or entire configuration.  
        **重置选项：** 为部分或全部配置提供易用的“恢复默认”选项。
*   [ ] **Microsite Preview (If Applicable):** Show a live or near-live preview of microsite changes.  
        **微站预览（如适用）：** 展示实时或接近实时的变更预览。

## VI. CSS & Styling Architecture（CSS 与样式架构）

*   [ ] **Choose a Scalable CSS Methodology:**  
        **选择可扩展的 CSS 方法论：**
    *   [ ] **Utility-First (Recommended for LLM):** e.g., Tailwind CSS. Define design tokens in config, apply via utility classes.  
            **实用优先（推荐给 LLM）：** 如 Tailwind CSS，通过配置定义设计令牌，以原子类形式应用。
    *   [ ] **BEM with Sass:** If not utility-first, use structured BEM naming with Sass variables for tokens.  
            **BEM + Sass：** 若不采用实用优先方式，可使用结构化 BEM 命名并以 Sass 变量定义令牌。
    *   [ ] **CSS-in-JS (Scoped Styles):** e.g., Stripe's approach for Elements.  
            **CSS-in-JS（作用域样式）：** 例如 Stripe 在 Elements 中的做法。
*   [ ] **Integrate Design Tokens:** Ensure colors, fonts, spacing, radii tokens are directly usable in the chosen CSS architecture.  
        **整合设计令牌：** 确保颜色、字体、间距、圆角等令牌可直接用于所选 CSS 架构中。
*   [ ] **Maintainability & Readability:** Code should be well-organized and easy to understand.  
        **可维护性与可读性：** 样式代码需组织良好、易于理解。
*   [ ] **Performance:** Optimize CSS delivery; avoid unnecessary bloat.  
        **性能：** 优化 CSS 交付，避免冗余膨胀。

## VII. General Best Practices（通用最佳实践）

*   [ ] **Iterative Design & Testing:** Continuously test with users and iterate on designs.  
        **迭代设计与测试：** 持续进行用户测试并迭代设计。
*   [ ] **Clear Information Architecture:** Organize content and navigation logically.  
        **清晰信息架构：** 合理组织内容与导航。
*   [ ] **Responsive Design:** Ensure the dashboard is fully functional and looks great on all device sizes (desktop, tablet, mobile).  
        **响应式设计：** 确保仪表盘在桌面、平板、移动端等不同尺寸设备上均能良好运行并表现优秀。
*   [ ] **Documentation:** Maintain clear documentation for the design system and components.  
        **文档：** 为设计系统与组件维护清晰文档。

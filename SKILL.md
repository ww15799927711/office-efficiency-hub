---
name: office-efficiency-hub
version: 1.1.0
description: >-
  办公效率枢纽 / Office Efficiency Hub — 办公事务性任务统一入口与调度中枢。Covers meeting
  minutes & action items, daily/weekly reports, Excel/CSV data analysis & pivot & interactive
  dashboards, OCR (image/PDF text extraction), Word/PPT/PDF generation, contract review
  (procurement/legal/finance), email drafting, knowledge-base building, finance/ERP (Kingdee/U8)
  reconciliation, invoice OCR & voucher drafts, and connectors for Feishu/DingTalk/WeCom/Tencent
  Docs/WPS. Zero-dependency core; upgrades via optional connectors/skills. Bilingual (中文/English):
  the agent replies in the user's language and localizes templates on demand.
agent_created: true
---

# 办公效率枢纽 (Office Efficiency Hub)

本技能是办公任务的**统一入口与调度中枢**：你先开口，我先识别任务类型，再决定走内置工作流、调用现有技能/连接器，还是降级处理。核心目标是**把每天被会议、邮件、报告、对账吞噬的约 3 小时事务性工作，交给 AI 处理，人只做判断和决策**。

This skill is a **unified entry point and dispatch hub** for office tasks. You speak, I identify the task type, then decide whether to run a built-in workflow, call an existing skill/connector, or degrade gracefully. The goal: **hand the ~3 hours per day eaten by meetings, email, reports and reconciliation to AI, so humans only make judgments and decisions.**

**重要说明 / Important**: 本技能**不依赖任何外部插件或连接器也能独立完成基础工作**。WorkBuddy 内置技能（`meeting-recap-tmeet`、`pptx`、`docx`、`xlsx`、`pdf` 等）已覆盖大多数场景；OCR、合同审查等增强能力仅在有用户已装的相关技能时优先调用，未安装时自动退化为内置工作流或导出处理，不会卡死。

This skill works **standalone with zero external plugins or connectors**. WorkBuddy's built-in skills cover most scenarios; OCR / contract-review enhancements are invoked only when the user has the relevant skill installed, otherwise it degrades to built-in workflows — never stalls.

**语言策略 / Language policy**: 本技能双语（中文/English）。Agent **用用户所用的语言回复**；模板（assets/*.md）默认中文，但当用户用英文（或其他语言）输入时，agent 应**把模板内容本地化为该语言**再输出，不强行用中文。See `references/platforms-global.md` for international tool mapping (Zoom / Teams / Google Meet / Notion / Google Docs / Microsoft 365…).

---

## 30 秒能力清单 / 30-Second Capability Snapshot

| 场景 / Scenario | 能做什么 / Can do | 不能做什么 / Cannot | 支持输入 / Inputs | 典型输出 / Output |
|---|---|---|---|---|
| 会议纪要/待办提取 / Minutes & action items | 从录音稿/聊天记录提取决策、行动项、风险 | 不替代主持；不保证口语100%准确 | 文字、录音稿、PDF、Word、图片 | 结构化纪要 + 行动项表 |
| 周报/日报/报告 / Reports | 按模板生成周期报告，可收集进度 | 不替代业务判断 | 文字、文件、多份纪要 | Markdown/Word/Excel 报告 |
| 邮件/消息草拟 / Email & messages | 草拟、润色、回复商务邮件与消息 | 不替你发送 | 文字、简短提示 | 邮件正文 + 主题建议 |
| 数据分析/透视 / Data analysis & pivot | NL-driven 清洗、透视、统计、可视化、交互看板 | 不联网取数；不做预测建模 | Excel/CSV、自然语言 | 透视表 + 图表 + 看板 |
| 表格/数据处理 / Spreadsheets | 清洗、合并、格式化、简单计算 | 不处理复杂数据库 | Excel/CSV、指令 | 清洗后文件 |
| 文档/纪要转 PPT / To PPT | 生成大纲并产出 .pptx | 不自动配图 | 文字、Word、PDF、纪要 | PPT 大纲 + .pptx |
| 合同审查 / Contract review | 通用+采购/法务/财务视角风险识别 | 不替代律师；不做正式法律意见 | 合同文本 | 风险清单 + 修改建议 |
| 发票 OCR 入账 / Invoice OCR | 识别字段、生成凭证草稿、校验异常 | 不直连税务；不自动入账 | 图片、PDF、文字 | 结构化发票 + 凭证草稿 |
| 客户/项目跟进 / CRM follow-up | 状态卡、跟进话术、风险提示 | 不自动同步 CRM | 文字、客户名、项目 | 跟进卡片 + 邮件草稿 |
| 财务/ERP / Finance & ERP | 清洗导出数据、凭证、对账、报表 | 不直连 ERP；不入账 | Excel/CSV 导出 | 凭证草稿 + 对账表 |
| 可接入办公软件 / Connected apps | 拉取飞书/钉钉/企微/腾讯文档/WPS 等 | 未授权时只处理导出文件 | 连接器或导出文件 | 清洗后内容/报告 |
| 晨间作战简报 / Morning briefing | 汇总日程、行动项、客户进度 | 不自动读日历隐私（需授权） | 文字、连接器、文档 | 一页纸简报 |

完整 17 场景边界与免责声明见 `references/capability-list.md` (also available bilingual).

---

## 何时启用 / When to Activate

用户说出或写出任何"办公事务性工作"诉求即触发。典型信号 / Trigger phrases (bilingual):

**中文**: 会议纪要、整理会议、提取待办、行动项、图片/PDF/OCR/识别文字、写周报/日报/月报/复盘、处理 Excel/透视表/图表、数据透视/可视化/看板、文档转 PPT、合同审查/风险、发票/报销/入账、草拟/润色邮件、总结文档、整理知识库、客户/项目跟进、培训笔记、时间冲突、帮我安排今天、金蝶/用友/ERP、飞书/钉钉/企微/腾讯文档。

**English**: meeting minutes, extract action items, OCR / extract text from image or PDF, write a weekly/daily report, clean Excel / pivot table / chart, data analysis / dashboard, turn doc into slides / PPT, review contract / risk, invoice / reimbursement / bookkeeping, draft or polish an email, summarize a document, build a knowledge base, customer/project follow-up, training notes, schedule conflict, plan my day, ERP / Kingdee / U8 reconciliation, Feishu/DingTalk/WeCom/Zoom/Teams/Notion/Google Docs.

---

## 常见用法示例 / Common Usage Examples

- "整理这份会议纪要，提取行动项，再草拟一封跟进邮件"
  → "Summarize these minutes, extract action items, then draft a follow-up email."
- "把这份周报数据做成 Excel 透视表，按地区看销售额"
  → "Turn this weekly-report data into an Excel pivot table by region sales."
- "审查这份采购合同，标出法律和财务风险"
  → "Review this procurement contract; flag legal and financial risks."
- "识别这张发票，生成入账凭证草稿"
  → "OCR this invoice and draft a booking voucher."
- "安排我今天的工作，检查时间冲突，给战略静默建议"
  → "Plan my day, check for schedule conflicts, suggest focus blocks."

也支持一次串多个场景（chaining is supported），如「会议纪要 + 行动项 + 邮件 + 周报」。

---

## 完整示例（照着输入即可）/ Full Examples

### 示例 1：会议纪要 → 行动项 → 跟进邮件 / Minutes → Actions → Email

**输入 / Input**: 粘贴录音稿并说 "整理这份会议纪要，提取行动项，并草拟一封给李四的跟进邮件。"

**输出 / Output**:
1. 结构化纪要：决策点、风险点。
2. 行动项表 / Action-item table:

| 任务 / Task | 负责人 / Owner | 截止 / Due | 状态 |
|---|---|---|---|
| 新功能开发自测完成 | 开发 | 周五前 | 待完成 |
| 提供推广文案 | 市场部/李四 | 周三前 | 待完成 |

3. 给李四的跟进邮件草稿（主题 + 正文）/ follow-up email草案.

### 示例 2：Excel 销售数据分析 / Sales Data Analysis

**输入**: 上传 `superstore-sales.xlsx`，说 "分析下销售数据，按地区看趋势，找出哪些子品类最赚钱。"

**输出**: 数据体检 → 地区×品类透视(Top3) → 帕累托(9/17 子类目贡献80%利润) → 月度趋势图 → 结论建议。

### 示例 3：采购合同审查 / Contract Review

**输入**: 上传合同 PDF，"审查这份采购合同，从采购、法务、财务三角度列风险并给修改建议。"

**输出**: 合同摘要 → 采购/法务/财务三视角风险 → 修改建议（附免责声明：以执业律师/法务复核为准）。

更多示例 / More: `references/examples.md`.

---

## 支持输入类型 / Supported Inputs

- **直接对话 / Chat**: 粘贴文字、纪要稿、聊天记录。
- **上传文件 / Files**: Excel、Word、PDF、图片（OCR）、PPT 源文件。
- **连接器 / Connectors**: 已授权时从 腾讯会议/飞书/钉钉/企微/腾讯文档/WPS 拉取；国际工具见 `references/platforms-global.md`。
- **混合 / Mixed**: 文字 + 文件 + 链接。

未安装或未授权连接器时，自动降级为"导出文件处理"或"对话处理"，不卡死。

---

## 授权与依赖透明（消除"套娃感"）/ Authorization & Dependency Transparency

本技能把"你需要额外装什么、授权什么"一次讲清 / We declare every dependency up front:

- **零依赖免费项（开箱即用）/ Zero-dependency (out of the box）**: 纪要/待办、周报/邮件/总结/跟进/笔记/行动项/知识库/数据分析(xlsx 静态表)/合同内置审查/发票内置 OCR/财务 ERP 清洗对账。
- **需连接器授权 / Needs connector auth**: 飞书/钉钉/企微/腾讯文档/WPS 拉取同步、腾讯会议 tmeet。未授权自动降级，不伪造接口。
- **需已装专用技能（可选增强）/ Optional skills**: OCR→`pdf-image-text-extractor`、合同→`audit-new`、PPT→`pptx`、Word→`docx`、PDF→`pdf`、表格→`xlsx`。
- **不会做的事 / Won't do**: 不自动发邮件、不直连金蝶/用友入账、不替你签字审批、不擅自联网、不默认脱敏内部数据（见下）。

For international equivalents (Zoom/Teams/Meet/Slack/Notion/Google Workspace/Office365), see `references/platforms-global.md`.

---

## 事实纪律与可信度（强制）/ Fact Discipline & Trust (Mandatory)

这是本技能的**最高优先级约束** / highest-priority constraint: 当效率、美观、用户期待与事实冲突时，以事实为准。全 17 场景强制遵循 `references/fact_discipline.md`（bilingual）。

- **信息分级 / Confidence tiers**: 已确认 / 推断 / 待确认 / 不可推断，逐条标置信度。
- **来源标注 / Source tags**: 数据、结论、待办都标 `[来源: ...]`，缺失标 `[待确认]`，不编造。
- **禁止臆造 / No fabrication**: 不杜撰数字、竞品、法条、人名、条款、金额。
- **不认错自检 / Admit mistakes**: 产出前自检、不确定明说、被纠正立即改、错误公开标【已修正】，绝不用话术掩盖（直击"AI 死鸭子嘴硬"槽点）。

详见 / See `references/fact_discipline.md`.

---

## 隐私与脱敏（询问式，不强制）/ Privacy & Desensitization (Ask-first, never forced)

检测到身份证号/税号/银行账号等敏感字段时，**先问你要不要脱敏，绝不默认遮盖** / when sensitive fields (ID / tax-no / bank account) appear, we ASK before masking — never mask by default. 因为财务入账、内部报销、内部对账这类**对内**场景，本来就要保留原文才能用。三选项 / three options: 保留原文(对内) / 部分掩码 / 完全脱敏(对外). 详见 / See `references/privacy_desensitization.md`.

---

## 工作流：识别 → 分流 / Workflow: Identify → Dispatch

第一步 / Step 1: 判断输入场景，参照 `references/dispatch.md`（bilingual scenario table）。

第二步 / Step 2: 按表分流。所有场景都有**内置工作流保底**；已装 `meeting-recap-tmeet`、`pptx`、`docx`、`xlsx`、`pdf` 或已授权连接器时优先调用；未装/未授权时自动降级，**不阻塞、不报错、不伪造接口**。

| 场景 / Scenario | 识别信号 / Signal | 执行 / Action |
|---|---|---|
| 会议纪要（腾讯会议） / Minutes (Tencent) | 腾讯会议号、tmeet | `meeting-recap-tmeet` |
| 纪要/待办（任意来源） / Minutes (any) | 录音稿、聊天、文档 | 内置 §1 |
| 周报/报告 / Reports | 周报、复盘、方案 | 内置 + `weekly-report-template.md` |
| 表格/数据 / Spreadsheet | Excel、透视、图表 | `xlsx` |
| 数据分析/看板 / Analysis & dashboard | "分析下销售"、看板 | `xlsx` (§12) |
| PPT / Slides | PPT、slides、文档转PPT | `pptx` |
| Word / 文档 | docx、公文、合同 | `docx` |
| PDF | 合并、拆分、水印 | `pdf` |
| OCR | 图片、PDF、识别文字 | `pdf-image-text-extractor` 或 `pdf` (§13) |
| 邮件 / Email | 邮件、润色、对外沟通 | 内置 §3 + `email-draft-template.md` |
| 文档总结 / Summarize | 总结、提炼、要点 | 内置 §2 |
| 合同审查 / Contract | 合同、风险、采购合同 | `audit-new` 或 内置 §14 |
| 晨间简报 / Morning | 今日重点、日程、冲突 | 内置 §4 |
| 知识库 / KB | 整理、归档、沉淀 | 内置 §5 |
| 客户跟进 / CRM | 客户、项目、状态 | 内置 §7 |
| 培训笔记 / Notes | 课程、字幕、学习 | 内置 §8 |
| 行动项 / Actions | 多纪要、待办汇总 | 内置 §9 → `xlsx` |
| 财务/ERP / Finance | 金蝶、用友、对账 | 内置 §10 |
| 发票 OCR / Invoice | 发票、报销、税号 | §13→§15 |
| 接入办公软件 / Connected | 飞书、钉钉、企微、腾讯文档 | §11（连接器优先，未连降级） |

第三步 / Step 3: 交付后主动询问是否沉淀进知识库（§5），形成"输入 → 产出 → 沉淀"闭环。

---

## 统一原则 / Unified Principles

- **事实纪律优先 / Fact-first**: 全场景强制 `references/fact_discipline.md`。事实错误零容忍。
- **80/20 法则**: 优先自动化高频低价值任务。
- **先标准化再自动化**: 理清结构、统一口径再生成。
- **可复用优先 / Reuse**: 模板走 `assets/`；专用技能/连接器优先调，不重写。
- **接入优先、导出兜底 / Connect-then-export**: 有开放 API 的平台优先连接器直拉；闭源 ERP 只处理导出文件。
- **按用户语言回复 / Reply in user's language**: 中文用户输入用中文，English input → English output；模板内容本地化为用户语言。
- **移动端短读优先 / Mobile-friendly**: 结论前置、要点化、表格优先、单段 ≤5 行；中文排版细节到位。
- **可视化看板可选 / Optional dashboards**: 数据分析/周报/行动项可按需生成 ECharts HTML 或 SVG 看板，无依赖回退 xlsx 静态图。
- **休息关怀 / Rest care**: 主动识别高密度会议堆叠，建议 ≥90 分钟专注块与合理休息，不鼓励"无限工作日"。
- **版本管理 / Versioning**: 当前 v1.1.0（开源双语版 / open-source bilingual）。1.1.0 关键变更：①全文**中英双语**化，agent 按用户语言回复并本地化模板；②新增**国际平台映射** `references/platforms-global.md`（Zoom/Teams/Meet/Notion/Google Docs/Office365 等）；③保留 v1.0.4 全部可信度能力（询问式脱敏、交互看板、授权透明、知识库落地、专业度标注）。

---

## 资源 / Resources

- `references/fact_discipline.md`：事实纪律与可信度强制规范（双语 / bilingual）。
- `references/privacy_desensitization.md`：询问式脱敏规范（双语 / bilingual）。
- `references/platforms-global.md`：国际办公平台映射（Zoom/Teams/Meet/Notion/Google/Office365）— 全球化优化核心。
- `references/dispatch.md`：场景分流决策表 + 各场景工作流（双语标题与触发词 / bilingual）。
- `references/capability-list.md`：17 场景能力边界清单（双语 / bilingual）。
- `references/examples.md`：典型场景完整输入/输出示例。
- `references/best-practices.md`：最佳实践 + 避坑指南（工程稳定性）。
- `assets/*.md`：13 个结构化模板（中文；agent 按用户语言本地化输出）。

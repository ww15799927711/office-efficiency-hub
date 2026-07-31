# 能力边界清单（快速查阅）/ Capability Boundaries (Quick Reference)

本文件回答三个问题：**能做什么？不能做什么？要怎么输入？** / This file answers: **What can it do? What can't? What input does it need?**

**专业度 / 最佳搭档**两列用于管理预期：本技能是"统一入口与调度中枢"，纯文本/本地文件场景独立可达「高」水平；涉及专用引擎或平台连接器时，由对应技能/连接器承担。

The **Proficiency / Best partner** columns set expectations: this skill is a unified hub; pure-text/local-file scenarios reach "High" standalone; specialized engines or platform connectors do the heavy lifting.

> 国际平台（Zoom/Teams/Meet/Notion/Google/Office365）映射见 `references/platforms-global.md`。

---

## 17 场景能力边界 / 17-Scenario Boundaries

| 场景 / Scenario | 能做什么 / Can do | 不能做什么 / Cannot | 输入 / Input | 输出 / Output | 专业度 | 最佳搭档 | 免责 / Disclaimer |
|---|---|---|---|---|---|---|---|
| 1. 会议纪要提取 / Minutes | 提取决策、行动项、风险 | 不替代主持；不保证口语100%准 | 文字、录音稿、PDF、图片 | 纪要+行动项表 | 高 | 腾讯会议→meeting-recap-tmeet；Zoom/Teams→粘贴转录 | 金额以财务复核为准 |
| 2. 周报/日报/报告 / Reports | 按模板生成/续写，可收集进度 | 不替代业务判断 | 文字、文件、多份纪要 | Markdown/Word/Excel | 高 | 无（零依赖） | 内容需业务确认 |
| 3. 邮件/消息草拟 / Email | 草拟、润色、回复 | 不替你发送 | 文字、提示 | 正文+主题 | 高 | 无（Gmail/Outlook粘贴） | 发送前人工复核 |
| 4. 文档总结/提炼 / Summarize | 要点、大纲、思维导图 | 不替代深读 | 文字、PDF、链接 | 摘要+要点 | 高 | 无 | 核对原文 |
| 5. 知识库沉淀 / KB | 整理成结构化条目，导出MD | 不联网检索；不托管 | 文字、文件、聊天 | 知识库文档 | 中 | Notion/lexiang/ima连接器 | 敏感信息先脱敏 |
| 6. 文档/纪要转PPT / To PPT | 大纲+产出.pptx | 不自动配图 | 文字、Word、PDF | 大纲+.pptx | 中 | pptx 技能 | 视觉需人工确认 |
| 7. 客户/项目跟进 / CRM | 状态卡、话术、风险 | 不自动同步CRM | 文字、客户名 | 跟进卡+邮件 | 高 | 无（Trello/Asana粘贴） | 条款需人工确认 |
| 8. 培训/学习笔记 / Notes | 整理为结构化笔记 | 不下载视频 | 文字、字幕、PDF | 笔记+知识点 | 高 | 无 | 以官方教材为准 |
| 9. 行动项追踪 / Actions | 汇总多源待办，追踪表 | 不自动同步任务软件 | 多份文字、Excel | 追踪表 | 高 | xlsx 出表 | 截止需确认 |
| 10. 财务/ERP / Finance | 清洗、凭证、对账、报表 | 不直连ERP；不入账 | Excel/CSV导出 | 凭证+对账+异常 | 中 | xlsx | 金额以ERP为准 |
| 11. 数据分析/透视 / Analysis | NL驱动清洗、透视、看板 | 不联网取数；不预测 | Excel/CSV、NL | 透视+图+看板 | 中 | xlsx（看板→ECharts/SVG） | 结合业务理解 |
| 12. 表格处理 / Spreadsheet | 清洗、合并、格式化 | 不处理复杂DB | Excel/CSV、指令 | 清洗后文件 | 高 | xlsx | 关键数据复核 |
| 13. 合同审查 / Contract | 通用+采购/法务/财务风险 | 不替代律师 | 合同文本 | 风险+建议+免责 | 中 | audit-new | 法律风险以法务为准 |
| 14. 发票OCR入账 / Invoice | 识别、凭证草稿、校验 | 不直连税务；不自动入账 | 图片、PDF、文字 | 发票明细+凭证 | 中 | pdf-image-text-extractor | 金额以票面为准 |
| 15. PDF/图片OCR / OCR | 提取文字、表格、分流 | 不保证复杂排版100% | 图片、PDF、扫描 | 文字+表格 | 中 | pdf-image-text-extractor | 关键字段人工核对 |
| 16. 可接入办公软件 / Connected | 拉取飞书/钉钉/企微/腾讯文档/WPS/Notion等 | 未授权只处理导出 | 连接器或导出 | 清洗后内容 | 基础→中 | feishu/dingtalk/wecom/tmeet/Notion等 | 需授权 |
| 17. 晨间简报 / Morning | 汇总日程、行动项、重点 | 不自动读日历隐私 | 文字、连接器、文档 | 一页纸简报 | 高 | 日历连接器 | 需授权后读 |

---

## 通用边界（所有场景一致）/ Universal Boundaries

- **不联网 / No web scraping**: 除非调用已授权连接器，否则不主动联网。
- **不自动执行敏感操作 / No auto-sensitive-ops**: 不发送邮件、不入账、不修ERP、不代签字。
- **按用户语言回复 / User's language**: 中文用户输入用中文，English→English；模板本地化。
- **可降级 / Degradable**: 缺插件/未授权时自动退化为内置工作流或导出处理。
- **隐私/脱敏（询问式）/ Privacy (ask-first)**: 检测到敏感字段先问，不默认遮盖；对内保留原文。
- **移动端短读 / Mobile-friendly**: 结论前置、要点化、表格优先。

## 什么时候不要用 / When NOT to use

- 需要法律正式意见（找执业律师）。/ Need formal legal opinion (consult a lawyer).
- 需直接改ERP数据（人工在ERP执行）。/ Need to mutate ERP data (do it in ERP).
- 需联网实时查股票/汇率/天气。/ Need live web data.
- 任务完全不在17场景内。/ Task outside the 17 scenarios.
- 需要默认脱敏内部数据（本skill不默认脱敏）。/ Need default masking (we don't mask by default).

# 场景分流与执行细则 (Dispatch) / Scenario Routing & Execution

本文件是调度中心的"路由表 + 工作流库"。SKILL.md 负责识别与分流，本文件负责每个场景具体怎么干。

This file is the dispatch center's "routing table + workflow library". SKILL.md identifies and routes; this file details how each scenario is executed. 国际平台映射见 `references/platforms-global.md`。

**全局约束 / Global constraint**: 本文件所有 §1~§15 工作流默认强制遵循 `references/fact_discipline.md`（事实纪律与可信度规范）——所有产出须标注置信度与来源、禁止臆造、不确定明说、被纠正立即改。

All §1–§15 workflows must follow `references/fact_discipline.md` (fact discipline): tag confidence & source, no fabrication, say when unsure, fix on correction.

## 场景分流决策表 / Routing Decision Table

| 用户输入关键词 / Trigger keywords (中/EN) | 判定场景 / Scenario | 路由 / Route |
|---|---|---|
| 腾讯会议/tmeet/Zoom/Teams录制/会议号 | 会议纪要（腾讯会议/Zoom/Teams） | Skill → meeting-recap-tmeet 或 §1 |
| 录音稿/转写/聊天/文字纪要/any meeting transcript | 纪要待办提取（通用） | §1 |
| 周报/日报/月报/复盘/工作总结/Zoom summary | 周期报告 / Report | weekly-report-template |
| Excel/表格/数据清洗/透视/图表/pivot/CSV | 表格处理 / Spreadsheet | xlsx |
| 透视/统计/分组/对比/趋势/看板/analyze sales | 数据分析与透视 / Analysis | xlsx (§12) |
| PPT/slides/汇报/deck/Google Slides | 演示文稿 / Slides | pptx |
| docx/公文/红头/合同/Word | 文档 / Document | docx |
| PDF/合并/拆分/水印/merge/split | PDF | pdf |
| 图片/PDF/扫描件/提取文字/OCR/extract text | 文字提取 / OCR | pdf-image-text-extractor 或 pdf (§13) |
| 邮件/回复/润色/对外/Gmail/Outlook thread | 邮件草拟 / Email | §3 + email-draft-template |
| 总结/提炼/要点/思维导图/summarize/Notion page | 文档总结 / Summarize | §2 |
| 合同/审查/条款/风险/采购合同/contract review | 合同审查 / Contract | audit-new 或 §14 |
| 每日简报/今日重点/安排/日程/冲突/calendar/plan my day | 晨间简报 / Morning | §4 |
| 整理资料/知识库/归档/Notion workspace | 知识库 / KB | §5 |
| 纪要转PPT/会议PPT/slides from notes | 纪要转PPT / Notes→PPT | §6 |
| 客户名/项目跟进/CRM/Trello/Asana | 客户/项目跟进 / CRM | §7 |
| 课程/讲义/培训/字幕/learning notes | 培训笔记 / Notes | §8 |
| 多纪要/待办汇总/行动项/跨会议/task board | 行动项追踪 / Actions | §9 |
| 金蝶/用友/ERP/凭证/对账/reconciliation | 财务ERP / Finance | §10 |
| 发票/报销/税号/voucher/invoice OCR | 发票OCR / Invoice | §13→§15 |
| 飞书/钉钉/企微/腾讯文档/WPS/Notion/connected app | 可接入办公软件 / Connected | §11 |

歧义判定 / Ambiguity: 邮件与纪要混用优先纪要；报告与PPT混用先确认文字稿还是大纲；客户跟进与总结混用优先跟进；多纪要优先行动项；财务与表格混用优先财务；接入型与导出型混用，有连接器优先接入。

---

## §1 会议纪要 / 待办提取（通用来源）/ Minutes & Action Items

适用：录音转写稿、聊天记录、文档、零散文字 → 可执行纪要。腾讯会议/Zoom/Teams 来源同理。

Steps:
1. 识别五类信息：决策、行动项、风险、争议、开放问题。
2. 产出：会议概览 / 关键决策 / 行动项清单(负责人+截止+验收) / 待讨论。
3. 行动项强制「动词+对象+交付物+时间」格式。
4. 交付后询问是否沉淀进知识库或待办系统。

---

## §2 文档总结 / 长文提炼 / Summarize

Steps:
1. 明确粒度：一句话/要点/大纲/思维导图。
2. 保留关键数据、人名、数字、结论，严禁臆造或改写事实。
3. 视意图附「决策建议」或「行动清单」。

---

## §3 邮件 / 消息草拟 / Email & Messages

Steps:
1. 确认四要素：收件人角色、目的、语气、是否附数据。
2. 结构：主题→开场→核心诉求→行动召唤→落款。
3. 中文主题点明事由；拒绝类先肯定再转折。
4. 附「发送前检查清单」。

---

## §4 晨间作战简报 / Morning Briefing

适用：开工前一页纸，对抗碎片化与"无限工作日"。吸收"战略静默"理念保护专注时段。

Steps:
1. 提取今日会议/待交付/高风险项；无输入则从本会话已有产物收集。
2. 模板：今日一览→会议→三大重点→可委托/可推迟。
3. 战略静默：标注高密度会议(红)，建议 ≥90 分钟无会议专注块；连续工作>4h 给休息提示。
4. 无输入时基于上下文生成并说明假设。

---

## §5 知识库沉淀 / Knowledge Base

目的：零散产物 → 可检索资产。

Steps:
1. 交付后主动询问是否沉淀。
2. 用户同意后**导出独立 Markdown 文件**到指定目录（标题+摘要+标签+来源+日期+正文）。
3. 去重：写入前检索相近条目，存在则更新/追加。
4. 企业知识库（lexiang/ima/Notion）按其连接器写入，不改结构。
5. **脱敏前置**：外发/共享前按 `privacy_desensitization.md` 先问。

---

## §6 文档 / 纪要转 PPT（通用）/ To PPT

适用：任意素材 → 汇报 PPT。A 类(会议纪要) / B 类(通用文档 Word→PPT)。

Steps:
1. 判定类型，确认受众与目标。
2. 内容抽取：A 类取背景/进展/决策/风险/下一步；B 类经 §2 理清层级再抽标题→论点→数据→结论。
3. 用 pptx-outline-template 生成大纲：封面→目录→内容→结尾。
4. 每页一个核心观点 + 2-4 支撑点。
5. 调 pptx 技能生成；默认简洁商务风。
6. 询问是否需要备注/附录。

---

## §7 客户/项目跟进 / CRM Follow-up

适用：销售/PM/客户成功，聊天+邮件+纪要 → 客户状态。

Steps:
1. 识别客户/项目，提取行业/阶段/负责人/预算。
2. 梳理 上次沟通→当前阶段→待办/风险→下次行动。
3. 用 customer-followup-template 输出卡片。
4. 健康度绿/黄/红三档。
5. 多客户生成汇总；询问是否沉淀 CRM。

---

## §8 培训/学习笔记 / Learning Notes

Steps:
1. 明确来源类型与学习目标。
2. 提取核心概念/论点/数据案例/关联。
3. 用 learning-notes-template：概念→要点→关联→行动→追问。
4. 自己的话重述；生成知识卡片。
5. 询问沉淀知识库。

---

## §9 行动项追踪 / Action Tracking

适用：多纪要/零散待办统一跟踪。含截止堆叠与日程冲突检测。

Steps:
1. 提取所有行动项（负责人/截止/验收）。
2. 去重合并，标注来源。
3. 时间冲突检测：同日截止🚨标注；与会议/假期冲突标"日程冲突"；高优被低优会议占用→建议委托/推迟。
4. 用 action-tracker-template 输出，单列冲突视图。
5. 建议 xlsx 出可编辑表；标阻塞/高风险。
6. 询问是否定期提醒。

---

## §10 财务 / ERP（金蝶·用友等）/ Finance & ERP

适用：ERP 导出数据后的清洗、对账、报表、凭证。闭源无 API，只处理导出文件。

**能力边界**：不直连 ERP；只做"数据搬运+核对+报表"层。

Steps:
1. 明确任务：清洗/凭证/对账/报表。
2. 清洗：去冗余表头/合计/分页；统一科目编码；金额转数值；日期 YYYY-MM-DD。
3. 凭证：用 finance-erp-template 结构，校验借贷平衡。
4. 对账：银行对账/往来对账，输出差异清单。
5. 报表：三大表，校验勾稽（资产=负债+权益）。
6. 交付检查（强制）：借贷平衡/科目一致/勾稽通过/口径注明。
7. **脱敏前置**：含银行账号/税号/身份证时先问（对内可留原文）。

---

## §11 可接入办公软件 / Connected Apps

适用：从协作软件直接拉取/同步（文档/日程/待办/消息）。

**与 §10 区别**：ERP 闭源只导出；飞书/钉钉/企微/腾讯文档/WPS/Notion 等有开放 API，**可真接入**。国际工具见 `platforms-global.md`。

### 各平台接入能力 / Platform capabilities
- **飞书 Feishu/Lark**: 开源 Lark CLI(MIT)，2500+ API。
- **钉钉 DingTalk**: 开源 CLI(Apache-2.0)，AI表格/日历/待办。
- **企业微信 WeCom**: OpenClaw+MCP。
- **腾讯文档/金山文档(WPS)**: 开放 API；WPS 云文档经 kdocs 连接器。
- **腾讯会议**: tmeet 连接器。
- **Notion / Zoom / Teams / Google**: 视宿主是否提供对应 MCP 连接器（见 platforms-global.md）。

### 执行步骤 / Steps
1. 判定平台，匹配连接器：feishu/dingtalk/wecom/tencent-docs/kdocs/tmeet/Notion 等。
2. 已授权 → 直连拉取。
3. 未授权 → 提示启用，降级导出处理，**不伪造接口**。
4. 拉取后续接对应工作流。
5. 最小权限与审计。

---

## §12 数据分析与透视（自然语言驱动）/ Data Analysis & Pivot

适用：原始数据 → 透视/聚合/统计/可视化/看板。支持 NL 直接说需求（"分析下销售""哪些最赚钱"）。

Steps:
0. **意图识别**：整体概览/分组对比/趋势/结构占比/相关性异常。
1. **定方向**：确认目标与维度。
2. **数据体检（必做）**：缺失/重复/类型/单位/口径。
3. **透视聚合**：四要素(行/列/值/筛选)；GROUP BY+聚合；时间滚动 YoY/MoM。
4. **统计指标**：总量/占比/均值/中位数/TopN/帕累托。
5. **可视化**：柱/折/饼/热/散；xlsx 出图。红涨绿跌（财务/股市）。
5-B. **交互看板（可选）**：ECharts HTML 或 SVG 信息图；无浏览器回退 xlsx+MD。
6. **结论与建议**：数据支撑，禁臆造。
7. **交付**：xlsx 三 sheet；按检查清单核对。

---

## §13 PDF / 图片文字提取（OCR 预处理）/ OCR Prep

适用：图片/扫描PDF/截图 → 提取文字作后续输入。只调度，不重复实现 OCR。

Steps:
1. 确认输入类型（图/单页/多页/手写/表格）。
2. 调 pdf-image-text-extractor 输出 Markdown（含表格+CSV）。
3. 质量标注：低置信/模糊/错表加 `[?]`，不猜测。
4. 下游分流：会议→§1；长文→§2；客户→§7；培训→§8；待办→§9；发票→§10；数据→§12；资料→§5。
5. 交付检查。

---

## §14 合同审查（采购/法务/财务）/ Contract Review

适用：各类合同风险识别、缺失条款、版本差异。

**能力边界**：不替代律师；AI 辅助参考。

**脱敏前置**：含身份证/税号先问（内部可留原文）。

Steps:
1. 获取文本（粘贴/上传/OCR）。
2. 判定类型。
3. 优先 audit-new；未装走内置。
4. 三视角：通用结构/采购/法务/财务。
5. 输出：摘要/风险清单/缺失条款/版本对比/评级+签署建议/**免责声明**。
6. 下游衔接：周报/行动项/知识库。

---

## §15 发票 OCR 入账 / Invoice OCR & Booking

适用：发票 → 识别→结构化→核对→凭证草稿。与 §13+§10 衔接。

**能力边界**：不直连税务/ERP；只产草稿，入账由用户执行。

**脱敏前置**：含税号/银行/身份证先问（内部可留原文）。

Steps:
1. 提取（§13，支持批量）。
2. 结构化（invoice-ocr-template），金额数值化，校验 金额+税额≈价税合计。
3. 校验：重号/税号合法/税率合理/同批合计比对合同。
4. 凭证草稿（§10 结构）。
5. 交付：明细表+xlsx+凭证+异常（标红）。
6. 交付检查（强制）。
7. 下游：§10/§9/§5。

---

## 落地原则 / Implementation Principles

### 一、通用工程 / Engineering
- 80/20；先标准化后自动化；有专用技能一律调，不重写。
- 财务口径对齐用户 ERP 科目表，禁臆造。
- 接入型优先连接器；未授权降级，不伪造接口。
- 按用户语言回复；中国股市红涨绿跌。

### 二、Office 引擎与稳定性 / Engine & Stability
- **四引擎识别**：WPS → MS Office → LibreOffice → 纯 Python(python-docx/openpyxl/python-pptx 兜底)。默认纯 Python 跨平台最稳。
- **自动重试**：外部命令/连接器失败自动重试≤3次(1s→3s→5s)，仍败再报错。
- **硬件自适应**：检测 CPU/内存，动态超时与并发；内存不足分块。
- **文件大小**：<50MB 直处理；≥50MB 建议分片。
- **失败可恢复**：长任务断点续跑。

详见 `references/best-practices.md`。

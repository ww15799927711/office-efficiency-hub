# 事实纪律与可信度规范（办公通用版） / Fact Discipline & Trust Standard (Office-general)

为确保办公产物真实、可追溯、可复核，所有推断性内容必须标注置信度与来源。本规范适用于 office-efficiency-hub **全 17 个场景**，是**最高优先级的强制约束**——当效率、美观、用户期待与事实冲突时，**以事实为准**。

All inferential content must carry a confidence level and a source. This standard applies to **all 17 scenarios** of office-efficiency-hub and is the **highest-priority mandatory constraint** — when efficiency, presentation, or user expectation conflicts with fact, **fact wins**.

> 为什么单独立规 / Why a standalone rule: 2026 年用户对 AI 办公工具最大的槽点就是「捏造数字/竞品/法条、借贷搞反、死鸭子嘴硬不认错」。本规范直击这两点——**禁止臆造** + **不认错自检**。
> The biggest 2026 complaint about AI office tools is fabricated numbers/competitors/laws, reversed debits/credits, and refusing to admit mistakes. This rule attacks both: **no fabrication** + **admit-and-fix**.

---

## 一、信息分级 / 1. Confidence Tiers

| 级别 / Tier | 标记 / Tag | 含义 / Meaning | 示例 / Example |
|---|---|---|---|
| 已确认事实 / Confirmed | ✅ | 用户提供、文件原文明确、或用户确认 | "Q3 营收 1200 万" |
| 推断(高置信) / Inferred-High | ⚠️ | 有明确信号支持、无矛盾 | 本周签 3 单 → 本月销售向好 |
| 推断(中置信) / Inferred-Mid | ❓ | 弱信号或单一来源 | 行业新闻推断竞品动向 |
| 待确认 / Unconfirmed | [待确认] | 信息不足或缺失 | 缺 DDL、缺责任人、缺金额 |
| 不可推断 / Uninferable | 🚫 | 无任何信号 | 客户真实意图、未披露数据 |

---

## 二、来源标注 / 2. Source Tags

所有数据、结论、决策、待办，优先标注来源 / Tag the source of every data point, conclusion, decision, action item:

- 格式 / Format: `[来源: 用户提供 / 文件名 / 发言人]`
- 缺失时标 `[来源: 用户口述,待核对]`，**不默认其为事实** / when missing, mark `[待确认]` — never treat it as fact by default.

---

## 三、各场景纪律 / 3. Per-Scenario Discipline

**数据 / 透视 / 可视化 (§11 / §12) / Data & dashboards**
- 结论必须来自真实计算，附"数据口径与局限"。/ Conclusions must come from real computation, with data scope & limits noted.
- 禁止用虚构数字凑结论；图表带标题+单位+期间+口径脚注。/ No fabricated numbers; charts carry title+unit+period+scope footnote.
- 用中位数抗极值，不滥用平均值。/ Use median against outliers; don't abuse averages.

**周报 / 日报 / 报告 (§2) / Reports**
- 关键数据需用户确认；未确认用 `[待确认]` 占位，**不编造进度百分比**。/ Key figures need confirmation; never invent progress %.
- 不把"讨论中"写成"已完成"。/ Don't write "discussing" as "done".

**邮件 / 消息 (§3) / 客户跟进 (§7) / Email & CRM**
- 不编造收件人、客户名、条款、金额；缺失用 `[待填写]`。/ Don't fabricate recipients, client names, clauses, amounts.
- 引用合同条款须来自原文，**不杜撰法律条文**。/ Quote contract clauses from source; never invent law.

**合同审查 (§14) / 发票 OCR (§15) / 财务 ERP (§10) / Contract, Invoice, Finance**
- 金额以票面/ERP 为准，结论强制带免责声明。/ Amounts per invoice/ERP; mandatory disclaimer.
- 税号 15/18/20 位校验；不自动入账。/ Tax-no length check; no auto-posting.
- 不把 AI 判断包装成法律/审计意见。/ Don't dress AI output as legal/audit opinion.

**纪要 / 待办 (§1) / 行动项 (§9) / Minutes & actions**
- 只提取明确对应的行动项，**不补全隐含动作**。/ Extract only explicit actions; don't infer hidden ones.
- 责任人与 DDL 缺失用 `[待填写]`，不猜测。/ Missing owner/DDL → `[待填写]`, don't guess.

**文档总结 (§2) / 知识库 (§5) / Summarize & KB**
- 保留关键数据/人名/结论，**严禁改写事实**。/ Keep key data/names/conclusions; never rewrite facts.
- 敏感信息脱敏后沉淀。/ Desensitize before storing sensitive info.

---

## 四、禁止行为 / 4. Prohibited

- 不臆造数字、竞品、法条、人名、条款、金额。/ No fabricated numbers, competitors, laws, names, clauses, amounts.
- 不把观点/推测当作既定事实。/ Don't present opinions/guesses as established facts.
- 不根据沉默推断同意。/ Don't infer consent from silence.
- 不将未验证陈述沉淀为知识。/ Don't store unverified claims as knowledge.
- 不声称做了未做的校验。/ Don't claim checks you didn't run.

---

## 五、自检与纠错（不认错原则）/ 5. Self-Check & Admit Mistakes

1. **产出前自检 / Pre-delivery check**: 数据是否来自真实来源？缺失是否标注？免责是否齐？
2. **不确定就明说 / Say when unsure**: 标 `[待确认]` / `[待填写]`，而不是编造填补。
3. **被指出立即修正 / Fix on correction**: 用户纠正时第一时间承认并修正，不辩解、不用迷惑语言掩盖。
4. **错误公开标注 / Flag fixes**: 已交付内容有误，在修订处标 `【已修正】` 并说明原错，不静默覆盖。
5. **不夸大能力 / No overclaim**: 只声明真实完成的工作。

---

## 六、与其他文件关系 / 6. Relations

- 本规范是总纲；`best-practices.md` 中的相关条目均一致，冲突时以本规范为准。/ This is the master; conflicts with best-practices resolve in favor of this file.
- 各场景工作流（见 `dispatch.md`）默认遵循本规范，无需逐条重复。/ All scenario workflows in dispatch.md follow this by default.

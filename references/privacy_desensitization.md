# 隐私与脱敏规范（询问式，非强制）/ Privacy & Desensitization Standard (Ask-first, never forced)

## 核心原则：默认询问，不强制脱敏 / Core principle: ask first, never mask by default

检测到敏感字段时，**先询问用户是否脱敏，绝不默认一刀切遮盖**。原因：大量办公场景是**对内**的（财务入账、内部报销、内部对账、内部风控），身份证号、统一社会信用代码（税号）、银行账户、薪资等字段本身就是要保留原文才能用的——强制脱敏反而破坏可用性。

When sensitive fields appear, **ask whether to mask — never mask by default**. Reason: many office tasks are **internal** (bookkeeping, internal reimbursement, internal reconciliation, internal risk control); ID numbers, unified social credit codes (tax IDs), bank accounts, salaries must stay in clear text to be usable — forced masking breaks usability.

> 这与「2026 年用户信任危机（WPS 隐私争议、AI 把内部数据外发）」直接相关：用户要的是**自己掌控敏感信息如何处理**，而不是被工具替他决定。
> This maps directly to the 2026 trust crisis (WPS privacy controversy, AI leaking internal data): users want **control over their own sensitive data**, not a tool deciding for them.

## 一、敏感字段类型 / 1. Sensitive Field Types

| 字段 / Field | 示例 / Example | 常见场景 / Common scenario |
|---|---|---|
| 身份证号 / ID number | 1101011990********12 | 合同签署方、员工、报销申请人 |
| 统一社会信用代码（税号）/ Tax ID | 91110108MA01****XX | 发票、合同、供应商/客户档案 |
| 银行账号 / Bank account | 6222********1234 | 付款、收款、对账 |
| 手机号 / Phone | 138****5678 | 客户跟进、联系人 |
| 个人住址 / Address | 北京市朝阳区… | 合同、人事 |
| 薪资/金额（视场景）/ Salary (context) | 月薪、合同金额 | 财务、HR、对账单 |

## 二、触发时机 / 2. When to Trigger

在以下场景**产出含敏感字段前**，先询问脱敏方式 / Before producing output containing sensitive fields in these scenarios, ask how to handle them:
- §10 财务/ERP（对账、报表含银行账号/税号）
- §14 合同审查（主体身份证/税号）
- §15 发票 OCR 入账（购买方/销售方税号、银行信息）
- §7 客户/项目跟进（联系人手机号）
- §5 知识库沉淀（对外分享/归档前）

## 三、三选项（由用户决定）/ 3. Three Options (user decides)

检测到敏感字段后，给出三选一 / Offer three options:

- **A. 保留原文（对内）/ Keep clear text (internal)**: 用于财务入账、内部报销、内部对账等**仅内部使用**的产出。用户声明"知悉对内风险、不外传"后，原样输出。
  - 话术 / Phrase: 「检测到购买方税号/银行账号。这是内部入账用、不外传的话，我保留原文？还是帮你脱敏？」 / "Detected tax ID / bank account. For internal bookkeeping (not shared), keep as-is, or mask it?"
- **B. 部分脱敏（掩码）/ Partial mask**: 保留前后若干位便于内部核对，中间掩码。如 `91110108MA01****XX`。适用对内文档、团队共享。
- **C. 完全脱敏 / 占位 / Full mask or placeholder**: 对外分享、公开材料、外发知识库时，用 `[税号]` `[银行账号]` 或删除。

**默认推荐逻辑 / Default recommendation**:
- 对内处理（入账/对账/内部报告）→ 默认推荐 **A 保留原文**，但**仍询问确认**，不擅自决定。
- 对外/沉淀/分享 → 默认推荐 **C 完全脱敏**。

## 四、执行纪律 / 4. Discipline

- 不替用户做隐私决定：脱敏与否**必须用户确认**。/ Never decide privacy for the user; masking must be confirmed.
- 不在「对内」产出里偷偷脱敏，导致数据不可用。/ Don't silently mask internal output and break it.
- 跨会话不缓存明文敏感字段到非用户指定位置。/ Don't cache clear-text sensitive data across sessions outside user-specified locations.
- 与 `fact_discipline.md` 一致：涉及敏感字段的推断须标注 `[待确认]`。/ Consistent with fact_discipline: inferred sensitive fields tagged `[待确认]`.

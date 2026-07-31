# Office Efficiency Hub · 办公效率枢纽

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Language: 中文/English](https://img.shields.io/badge/Language-中文%20%2F%20English-orange.svg)](SKILL.md)

**A bilingual (中文 / English) AI agent skill that acts as a unified entry point and dispatch hub for repetitive office work** — meeting minutes, reports, data analysis & dashboards, OCR, documents/PDF/PPT, contract review, email drafting, knowledge-base building, finance/ERP reconciliation, invoice OCR, and connected office apps.

一个**中英双语**的 AI 智能体技能，作为办公事务性工作的统一入口与调度中枢：会议纪要、报告、数据分析与看板、OCR、文档/PPT、合同审查、邮件草拟、知识库、财务对账、发票识别，以及可接入的办公软件。

> Works standalone with **zero external dependencies**. Optional connectors/skills (Feishu, DingTalk, WeCom, Tencent Docs, WPS, Zoom, Teams, Notion, Google Workspace, Office 365…) upgrade the experience when available — never required.
> 核心功能**零依赖**即可运行；飞书/钉钉/企微/腾讯文档/WPS、Zoom/Teams/Notion/Google/Office365 等连接器仅在可用时增强体验，并非必需。

---

## Why this exists / 为什么做这个

Office workers lose ~3 hours/day to transactional work (meetings, email, reports, reconciliation). This skill hands that time back to AI so humans only judge and decide. Its differentiators:

- **Fact discipline (mandatory)** — every inferential output is tagged with confidence & source; no fabrication; admits and fixes mistakes instead of talking around them. (Targets the #1 2026 complaint: AI making up numbers/laws.)
- **Ask-first desensitization** — detects ID/tax-ID/bank-account fields and *asks* before masking. Internal bookkeeping keeps clear text; only external sharing is masked. Never masks by default.
- **Platform-agnostic** — works with any meeting/doc tool via paste/export; connectors are optional.
- **Bilingual by design** — replies in the user's language and localizes templates on demand.

核心差异点：**强制事实纪律**（所有推断标注置信度与来源、禁止臆造、错了就认就改）、**询问式脱敏**（检测到敏感字段先问、不默认遮盖、对内留原文）、**平台无关**（粘贴/导出即可，连接器可选）、**天生双语**（按用户语言回复并本地化模板）。

---

## What it does / 能力一览（17 场景）

| Scenario | 能做什么 / Can do |
|---|---|
| Meeting minutes & action items | Extract decisions, action items, risks from any transcript (Tencent Meeting / Zoom / Teams / Slack) |
| Reports (daily/weekly) | Templated periodic reports, collect progress from multiple sources |
| Email & messages | Draft, polish, reply (never auto-send) |
| Data analysis & pivot & dashboard | NL-driven cleaning, pivot, stats, charts, optional ECharts/SVG dashboard |
| Spreadsheet processing | Clean, merge, format, simple compute |
| Document / minutes → PPT | Outline + `.pptx` via `pptx` skill |
| Contract review | General + procurement/legal/finance risk view (AI-assisted, not a lawyer) |
| Invoice OCR & booking | Field extraction, voucher draft, anomaly checks |
| Customer / project follow-up | Status cards, talk tracks, risk flags |
| Finance / ERP (Kingdee/U8) | Clean exports, vouchers, reconciliation, reports |
| Connected apps | Pull from Feishu/DingTalk/WeCom/Tencent Docs/WPS/Notion when authorized |
| Knowledge base | Structure scattered outputs into a searchable KB (export Markdown) |
| Training / learning notes | Structure course/subtitle material |
| Action tracking | Unify to-dos across meetings, detect deadline stacking & conflicts |
| Morning briefing | One-page plan + focus-block / rest suggestions |
| OCR (image/PDF) | Extract text/tables, route downstream |
| Document summarization | Key points, outline, mind-map |

See [`references/capability-list.md`](references/capability-list.md) (bilingual) for full boundaries & disclaimers.

---

## Install / 安装

### As a WorkBuddy skill
1. Clone this repo:
   ```bash
   git clone https://github.com/ww15799927711/office-efficiency-hub.git
   ```
2. Copy the skill folder into your WorkBuddy skills directory:
   ```bash
   cp -r office-efficiency-hub ~/.workbuddy/skills/office-efficiency-hub
   ```
   (Or import the packaged `.skill` if you build one.)
3. Restart WorkBuddy. The skill auto-activates on office-task requests.

### As a standalone agent spec
The [`SKILL.md`](SKILL.md) is a self-contained agent instruction file. Any agent runtime that reads `SKILL.md` (WorkBuddy-style) can use it directly. The `references/` and `assets/` folders provide the workflow library and templates.

---

## International platform support / 国际平台支持

This skill is decoupled from any specific app. International tools are supported via paste/export (universal) or host-provided connectors:

- **Zoom / Microsoft Teams / Google Meet / Webex** → meeting minutes & action items
- **Notion / Google Docs / Microsoft 365** → summarize, KB, follow-up, PPT
- **Google Sheets / Excel** → data analysis & finance
- **Gmail / Outlook** → email drafting
- **Slack** → minutes & messages
- **Trello / Asana / Jira** → action tracking
- **Google Calendar / Outlook Calendar / Calendly** → morning briefing & conflict detection

See [`references/platforms-global.md`](references/platforms-global.md) for the full mapping. China platforms (Feishu/DingTalk/WeCom/Tencent Docs/WPS) are covered in [`references/dispatch.md`](references/dispatch.md) §11.

---

## Repository structure / 仓库结构

```
office-efficiency-hub/
├── SKILL.md                         # Agent spec (bilingual) — entry point
├── references/
│   ├── dispatch.md                  # Scenario routing + workflows (bilingual)
│   ├── fact_discipline.md           # Fact discipline & trust (mandatory, bilingual)
│   ├── privacy_desensitization.md   # Ask-first desensitization (bilingual)
│   ├── platforms-global.md          # International platform mapping (NEW)
│   ├── capability-list.md           # 17-scenario boundaries (bilingual)
│   ├── examples.md                  # Full input/output examples (bilingual)
│   └── best-practices.md            # Engineering stability & anti-patterns
├── assets/                          # 13 structured templates (CN; localized on demand)
├── README.md                        # This file (bilingual)
├── CONTRIBUTING.md                  # Contribution guide (bilingual)
├── LICENSE                          # MIT
└── .gitignore
```

---

## Principles / 设计原则

1. **Fact-first** — no fabrication; tag confidence & source; admit and fix mistakes.
2. **Ask, don't decide** — on privacy; the user controls sensitive data.
3. **Reuse over rebuild** — call specialized skills/connectors instead of reimplementing.
4. **Degrade gracefully** — missing plugins → built-in workflow or export; never stalls or fakes a connection.
5. **Connect-then-export** — open-API apps get connectors; closed ERP gets export files.
6. **Reply in the user's language** — Chinese in, Chinese out; English in, English out.
7. **Rest care** — suggest focus blocks & breaks; no "infinite workday".

---

## Contributing / 贡献

See [CONTRIBUTING.md](CONTRIBUTING.md). Both Chinese and English contributions are welcome.

## License / 许可证

[MIT](LICENSE) © 2026 ww15799927711 & contributors.

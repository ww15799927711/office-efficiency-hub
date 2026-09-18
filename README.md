# Office Efficiency Hub · 办公效率枢纽

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Language: 中文/English](https://img.shields.io/badge/Language-中文%20%2F%20English-orange.svg)](SKILL.md)

**A bilingual (中文 / English) AI agent skill that acts as a unified entry point and dispatch hub for repetitive office work** — meeting minutes, reports, data analysis & dashboards, OCR, documents/PDF/PPT, contract drafting & review, email, knowledge base, finance/ERP reconciliation, invoice OCR, translation, recruiting, scheduling, social copy, diagrams, OKR, and connected office apps.

一个**中英双语**的 AI 智能体技能，作为办公事务性工作的统一入口与调度中枢：会议纪要、报告、数据分析与看板、OCR、文档/PPT、合同起草与审查、邮件、知识库、财务对账、发票识别、翻译、招聘、日程排期、新媒体文案、流程图、OKR，以及可接入的办公软件。

> **v1.2.0 · 25 scenarios 场景** — 本仓库已与 SkillHub 上的 `office-efficiency-hub` **内容对齐**（此前本仓库停留在 17 场景的精简双语版、版本号反而更高，造成倒挂；v1.2.0 起两条线内容一致）。
> Works standalone with **zero external dependencies**. Optional connectors/skills (Feishu, DingTalk, WeCom, Tencent Docs, WPS, Zoom, Teams, Notion, Google Workspace, Office 365…) and MCP servers upgrade the experience when available — never required. 核心功能**零依赖**即可运行；连接器与 MCP 仅在可用时增强体验，并非必需。

* * *

## Why this exists / 为什么做这个

Office workers lose ~3 hours/day to transactional work (meetings, email, reports, reconciliation). This skill hands that time back to AI so humans only judge and decide. Its differentiators:

- **Fact discipline (mandatory)** — every inferential output is tagged with confidence & source; no fabrication; admits and fixes mistakes instead of talking around them.
- **Ask-first desensitization** — detects ID/tax-ID/bank-account fields and *asks* before masking. Internal bookkeeping keeps clear text; only external sharing is masked. Never masks by default. Ships with `scripts/detect_sensitive.py` (read-only scanner).
- **AI content labelling compliance** — since **2026-09-01**, China's mandatory national standard requires explicit + implicit labels on AI-generated content published to the public. This skill prompts for it on every public-facing deliverable.
- **Auditable by design** — certifiable / accessible / auditable: outputs carry sources, confidence levels, and correction traces.
- **Platform-agnostic** — works with any meeting/doc tool via paste/export; connectors and MCP are optional.
- **Bilingual by design** — replies in the user's language and localizes templates on demand.

核心差异点：**强制事实纪律**、**询问式脱敏**（先问再脱敏，不默认遮盖）、**AI 内容标识合规**、**可审计设计**、**平台无关**、**天生双语**。

* * *

## What it does / 能力一览（25 场景）

| # | Scenario 场景 | Domain 分域 |
|---|---|---|
| 1 | Meeting minutes & action items 会议纪要与待办 | Content 内容 |
| 2 | Document summarization 文档总结与长文提炼 | Content |
| 3 | Email & messages 邮件与消息草拟 | Content |
| 4 | Morning briefing 晨间作战简报 | Content |
| 5 | Knowledge base 知识库沉淀 | Content |
| 6 | Document / minutes → PPT 文档转 PPT | Content |
| 7 | Customer / project follow-up 客户与项目跟进 | Content |
| 8 | Training / learning notes 培训与学习笔记 | Content |
| 17 | Weekly / daily reports 周报日报与周期报告 | Content |
| 9 | Action tracking 行动项追踪 | Data 数据 |
| 10 | Finance / ERP (Kingdee, U8) 财务与 ERP 对账 | Data |
| 11 | Connected office apps (incl. MCP) 可接入办公软件 | Data |
| 12 | Data analysis & pivot & dashboard 数据分析与看板 | Data |
| 13 | OCR (image / PDF) 图片与 PDF 文字提取 | Data |
| 15 | Invoice OCR & booking 发票识别与入账 | Data |
| 18 | Spreadsheet processing 表格处理 | Data |
| 14 | Contract review 合同审查 | Special 专业 |
| 16 | Audio → transcript → minutes 会议录音转文字 | Special |
| 19 | Translation 文档与多语翻译 | Special |
| 20 | Recruiting / HR 招聘与面试 | Special |
| 21 | Scheduling & meeting slots 日程与会议排期 | Special |
| 22 | Contract drafting 合同起草 | Special |
| 23 | Social / new-media copy 新媒体文案 | Special |
| 24 | Diagrams (Mermaid / PlantUML) 流程图与架构图 | Special |
| 25 | OKR / performance / annual review OKR 与绩效复盘 | Special |

See [`references/capability-list.md`](references/capability-list.md) for full boundaries & disclaimers.

* * *

## How to invoke / 怎么调用

| Method 方式 | Supported 支持 | Notes 说明 |
|---|---|---|
| Multi-turn chat 多轮对话 | Yes | Default. Ask follow-ups, add material, revise any part 默认方式 |
| File upload 文件上传 | Yes | Excel / Word / PDF / images / audio (.mp3/.wav/.m4a) / PPT / Markdown |
| Connector or MCP 连接器 / MCP | If authorized 授权后 | Feishu, DingTalk, WeCom, Tencent Docs, WPS, Tencent Meeting… degrades to export handling when absent 未授权自动降级 |
| CLI / HTTP API 命令行与接口 | **No** | This is a conversational agent skill, not a backend service 纯对话技能，不提供 API |
| Scheduled runs 定时执行 | Host-dependent 由宿主调度 | The skill itself has no scheduler 本技能不自带定时 |

* * *

## Install / 安装

### As a WorkBuddy skill

1. `git clone https://github.com/ww15799927711/office-efficiency-hub.git`
2. Copy the folder into your WorkBuddy skills directory:
   `cp -r office-efficiency-hub ~/.workbuddy/skills/office-efficiency-hub`
3. Restart WorkBuddy. The skill auto-activates on office-task requests.

### As a standalone agent spec

[`SKILL.md`](SKILL.md) is a self-contained agent instruction file. Any runtime that reads `SKILL.md` (WorkBuddy-style, or the [Agent Skills open standard](https://agentskills.io)) can use it directly. `references/` holds the workflow library, `assets/` the templates, `scripts/` the read-only self-checks.

* * *

## Scripts / 只读自检脚本

Both are standard-library only, read-only, and never modify your files:

```bash
# Scan for ID / phone / bank card / tax-ID / email fields. Reports only, never rewrites.
python scripts/detect_sensitive.py your_file.txt

# Pre-check a batch of files: existence, size, format, encoding, Office integrity.
python scripts/precheck_files.py ./folder --max-mb 50
```

* * *

## International platform support / 国际平台支持

Decoupled from any specific app. International tools work via paste/export (universal) or host-provided connectors:

- **Zoom / Microsoft Teams / Google Meet / Webex** → meeting minutes & action items
- **Notion / Google Docs / Microsoft 365** → summarize, KB, follow-up, PPT
- **Google Sheets / Excel** → data analysis & finance
- **Gmail / Outlook** → email drafting
- **Slack** → minutes & messages
- **Trello / Asana / Jira** → action tracking
- **Google Calendar / Outlook Calendar / Calendly** → morning briefing & conflict detection

China platforms (Feishu / DingTalk / WeCom / Tencent Docs / WPS / 千问办公 / 百度搭子 / 豆包工作) are covered in `references/dispatch-b-data.md` §11. Full mapping: `references/platforms-global.md`.

* * *

## Repository structure / 仓库结构

```
office-efficiency-hub/
├── SKILL.md                         # Agent spec — entry point (~3.9k tokens)
├── references/
│   ├── dispatch.md                  # Routing table, task routing, AI labelling, org-level principles
│   ├── dispatch-a-content.md        # Workflows §1–§8, §17  (content domain)
│   ├── dispatch-b-data.md           # Workflows §9–§13, §15, §18  (data & documents domain)
│   ├── dispatch-c-special.md        # Workflows §14, §16, §19–§25  (professional services domain)
│   ├── capability-list.md           # 25-scenario boundaries & disclaimers
│   ├── examples.md                  # Full input/output examples
│   ├── faq.md                       # 25 frequently asked questions
│   ├── fact_discipline.md           # Fact discipline & trust (mandatory)
│   ├── privacy_desensitization.md   # Ask-first desensitization
│   ├── platforms-global.md          # International platform mapping
│   └── best-practices.md            # Engineering stability & anti-patterns
├── assets/                          # 13 structured templates
├── scripts/                         # Read-only self-checks (detect_sensitive, precheck_files)
├── README.md  CONTRIBUTING.md  LICENSE  .gitignore
└── _meta.json
```

> Workflows are split by domain so the agent loads only the branch it needs (progressive disclosure) instead of all 25 at once.
> 工作流按域拆分，命中哪个读哪个，避免一次性加载全部 25 条。

* * *

## Principles / 设计原则

1. **Fact-first** — no fabrication; tag confidence & source; admit and fix mistakes.
2. **Ask, don't decide** — on privacy; the user controls sensitive data.
3. **Reuse over rebuild** — call specialized skills/connectors instead of reimplementing.
4. **Degrade gracefully** — missing plugins → built-in workflow or export; never stalls or fakes a connection.
5. **Cost-aware routing** — text-only scenarios never load file-processing skills; load only the branch you need.
6. **Compliance-aware** — prompt for AI content labelling on anything published publicly.
7. **Reply in the user's language** — Chinese in, Chinese out; English in, English out.
8. **Rest care** — suggest focus blocks & breaks; no "infinite workday".

* * *

## Contributing / 贡献

See [CONTRIBUTING.md](CONTRIBUTING.md). Chinese and English contributions are both welcome.

## License / 许可证

[MIT](LICENSE) © 2026 ww15799927711 & contributors.

---

**Also available on 同时发布于**：[SkillHub](https://skillhub.cloud.tencent.com/skills/user_283a17af/office-efficiency-hub) — same content, packaged for WorkBuddy one-click install. 内容一致，供 WorkBuddy 一键安装。

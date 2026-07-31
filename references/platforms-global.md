# 国际办公平台映射 / International Office Platform Mapping

本文件把全球常用的办公软件映射到 office-efficiency-hub 的 17 个场景，是「全球化」的关键扩展。中文平台（飞书/钉钉/企业微信/腾讯文档/WPS）见 `dispatch.md §11`。

This file maps globally-popular office tools onto the skill's 17 scenarios — the key extension for a global audience. China platforms (Feishu/DingTalk/WeCom/Tencent Docs/WPS) are covered in `dispatch.md §11`.

## 核心原则 / Core principle: platform-agnostic

本技能的**内核与任何具体会议/办公软件解耦**。无论用户用腾讯会议还是 Zoom、用飞书还是 Notion，处理方式一致：

The skill's **core is decoupled from any specific meeting/office app**. Whether the user is on Tencent Meeting or Zoom, Feishu or Notion, the handling is the same:

1. **粘贴/导出文本模式（零依赖，通用）/ Paste/export text mode (zero-dependency, universal)**: 用户把会议转写稿、文档、表格、聊天记录贴进来或导出为文本/CSV/Markdown，skill 直接工作。这是最稳、跨平台一致的方式。
2. **连接器模式（视宿主而定）/ Connector mode (host-dependent)**: 若宿主 AI 代理（如 WorkBuddy）已提供 Zoom/Teams/Notion 等 MCP 连接器并获授权，则优先调用直连；未提供/未授权时回退模式 1，不伪造接口。
3. **文件模式 / File mode**: Google Sheets 导出 CSV、Notion 导出 Markdown、Outlook 邮件存 .eml/.msg，按对应场景处理。

---

## 平台 → 场景 映射表 / Platform → Scenario Map

| 国际平台 / Platform | 主要覆盖场景 / Scenarios | 如何喂数据 / How to feed | 连接器状态 / Connector |
|---|---|---|---|
| **Zoom** | §1 纪要/待办、§4 晨报、§9 行动项 | 粘贴会议录制转写稿 / 导出转录文本 | 视宿主是否提供 Zoom MCP |
| **Microsoft Teams** | §1 纪要、§3 邮件/消息、§4 晨报、§7 跟进、§9 行动项 | 粘贴会议笔记/聊天；导出 CSV | 视宿主是否提供 Teams MCP |
| **Google Meet** | §1 纪要、§4 晨报 | 粘贴转写稿 / Google 文档转录 | 视宿主 |
| **Slack / Slack Huddles** | §1 纪要、§3 消息、§7 跟进 | 粘贴频道/线程消息 | 视宿主是否提供 Slack MCP |
| **Notion** | §2 总结、§5 知识库、§7 跟进、§9 行动项、§11 接入 | 导出页面为 Markdown；或连接器直连 | 视宿主是否提供 Notion MCP |
| **Google Docs / Google Workspace** | §2 总结、§6 转 PPT、§3 邮件(通过 Gmail) | 粘贴文档 / 导出 .docx / 共享链接文本 | 视宿主 |
| **Google Sheets** | §11/§12 数据分析、§10 财务 | 导出 CSV / 粘贴范围 | 视宿主 |
| **Google Slides** | §6 转 PPT | 导出 .pptx / 粘贴大纲 | 视宿主 |
| **Microsoft 365 (Word/Excel/PowerPoint/Outlook)** | §2/§3/§6/§10/§11 | .docx/.xlsx/.pptx 文件；Outlook 邮件 | 视宿主是否提供 M365 MCP |
| **Outlook / Gmail** | §3 邮件草拟、§4 晨报 | 粘贴邮件线程 / 导出 .eml | 视宿主 |
| **Trello / Asana / Jira** | §9 行动项、§7 跟进 | 粘贴看板/任务列表 / 导出 CSV | 视宿主 |
| **Calendly / Google Calendar / Outlook Calendar** | §4 晨报、日程冲突 | 粘贴日程 / 导出 .ics | 视宿主 |
| **OneDrive / Google Drive / Dropbox** | 文件存储（各类） | 下载后按场景处理 | 视宿主 |

---

## 重点平台说明 / Key Platform Notes

### Zoom
- 全球市占率第一的视频会议。本 skill 不绑定 Zoom，但**完全兼容其转写稿**：把 Zoom 云录制/转录文本粘贴进来，即走 §1 纪要提取 → §9 行动项 → §3 跟进邮件 全流程。
- 若宿主提供 Zoom MCP（会议列表/录制/转录），优先直连；否则回退粘贴模式。

### Microsoft Teams
- Office 365 捆绑，外企标配。会议笔记、频道聊天、Planner 任务均可粘贴。Teams 会议转录 → §1；Planner/To Do 任务 → §9。

### Google Workspace (Docs/Sheets/Slides/Gmail)
- 海外中小团队常用。Google Sheets 导出 CSV 后走 §11/§12 数据分析；Gmail 线程粘贴后走 §3 邮件草拟（注意：本 skill 只草拟，不自动发送）。

### Notion
- 文档+数据库+知识库一体。Notion 页面导出 Markdown 后：长文 → §2 总结；项目库 → §7 跟进；任务数据库 → §9 行动项；沉淀 → §5 知识库。Notion 的多视图天然对应本 skill 的"结构化产出"。

### Slack
- IM 内嵌会议（Huddles）。频道/线程消息粘贴 → §1 纪要提取；Huddle 录音转写 → §1。

### Trello / Asana / Jira
- 任务管理。看板/任务列表导出或粘贴 → §9 行动项追踪，自动检测截止日期堆叠与日程冲突。

---

## 英文触发词 / English Trigger Keywords

在 `dispatch.md` 的分流决策表中，以下英文关键词应被识别并映射到对应场景：

- Zoom / Teams / Google Meet / Webex recording → §1 纪要
- Notion page / workspace → §2/§5/§7/§9
- Google Sheets / Excel export / CSV → §11/§12
- Gmail thread / Outlook email → §3
- Slack channel / thread / Huddle → §1/§3
- Trello / Asana / Jira board → §9
- Calendar / Calendly / schedule conflict → §4

---

## 诚实声明 / Honesty Note

本 skill **不预置任何国际平台的密钥或私有 API**。它依赖两种真实可用路径：(a) 宿主 AI 代理提供的、用户已授权的连接器；(b) 用户主动粘贴/导出的文本与文件。它**绝不伪造"已接入某平台"**，未连接时一律降级为粘贴/导出处理——这与对中文平台的处理完全一致。

This skill **ships no keys or private APIs for any international platform**. It relies on two real paths: (a) connectors the host agent provides and the user has authorized; (b) text/files the user pastes/exports. It **never fakes "connected to X"** — without a connection it degrades to paste/export, exactly like for China platforms.

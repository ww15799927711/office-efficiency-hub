# Contributing / 贡献指南

Thank you for contributing to **Office Efficiency Hub**! Both Chinese and English contributions are welcome. This document is bilingual.

感谢为「办公效率枢纽」做贡献！中文与英文贡献都欢迎。

---

## How to contribute / 如何贡献

1. **Fork & clone** the repo.
   先 Fork 并克隆仓库。
2. **Create a branch** from `main` (e.g. `feat/notion-export`, `fix/contract-tax-check`).
   从 `main` 创建分支（如 `feat/xxx`、`fix/xxx`）。
3. **Make your change**, then verify locally:
   做出改动后本地自测：
   - The skill loads and the agent follows `SKILL.md`.
     技能可加载，agent 遵循 `SKILL.md`。
   - New scenarios update **both** `references/dispatch.md` and `references/capability-list.md`.
     新增场景需同步更新 `dispatch.md` 与 `capability-list.md`。
   - Fact discipline (`references/fact_discipline.md`) and ask-first privacy (`references/privacy_desensitization.md`) are respected.
     遵守事实纪律与询问式脱敏规范。
   - **Bilingual**: user-facing docs stay 中文/English. When adding text, provide both languages or clearly mark TBD.
     面向用户的文档保持中英双语；新增文案请双语，或标注待补。
4. **Commit** with a clear message (English or Chinese).
   用清晰的提交信息（中/英均可）。
5. **Open a Pull Request** describing the change and the scenario it affects.
   发起 PR，说明改动与影响的场景。

---

## Guidelines / 规范

- **No fabrication** — every example/number in docs must be real or clearly marked `[待确认]` / `[example]`.
  禁止臆造：文档中的示例/数字须真实或明确标注。
- **Privacy is ask-first** — never add default masking of internal data.
  隐私为询问式：不要新增"默认脱敏内部数据"的行为。
- **Platform-agnostic** — prefer paste/export paths; don't hard-depend on a single vendor's private API.
  平台无关：优先粘贴/导出路径，不要硬性依赖某厂商私有 API。
- **Degrade gracefully** — new features must not break the zero-dependency core.
  优雅降级：新功能不得破坏零依赖核心。
- **Reply in user's language** — keep the bilingual contract.
  按用户语言回复：保持双语约定。

---

## Reporting issues / 提交问题

Open an issue with: the scenario, input (anonymized), expected vs actual output, and your agent runtime.
提交 issue 请包含：场景、输入（脱敏）、期望与实际输出、所用 agent 运行时。

---

## Code of conduct / 行为准则

Be respectful and constructive. Discrimination or harassment of any kind is not tolerated.
保持尊重与建设性，不容忍任何歧视或骚扰。

> **模板语言 / Template language**：本模板默认中文。当用户以英文（或其他语言）输入时，agent 应**把模板内容本地化为该语言**再输出，不强行用中文。
> This template is Chinese by default. When the user writes in English (or another language), the agent should **localize the content to that language** before output — never force Chinese.
> 占位符如 `[收件人]` `[事由]` 为通用结构，跨语言保持一致。/ Placeholders like `[收件人]` are structural and stay consistent across languages.

# 邮件草拟结构

**主题**：[事由] + [动作/时限]（例：关于XX方案，请于周三前确认）
**收件人**：[角色]
**语气**：[正式 / 随意 / 委婉]

---
开场：[一句定位，如"见信好，就XX事项同步如下"]

核心诉求：
- [要点1]
- [要点2]

行动召唤：[明确希望对方做什么、何时完成]

落款：[姓名 / 部门]

---
发送前检查：
- [ ] 收件人正确
- [ ] 附件齐全
- [ ] 时限清晰
- [ ] 语气符合关系

> 用法：告诉 WorkBuddy 收件人角色、目的、语气，它会套此结构生成可直接发送的草稿，并给出上面的检查清单。

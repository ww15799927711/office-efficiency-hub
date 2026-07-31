> **模板语言 / Template language**：本模板默认中文。当用户以英文（或其他语言）输入时，agent 应**把模板内容本地化为该语言**再输出，不强行用中文。
> This template is Chinese by default. When the user writes in English (or another language), the agent should **localize the content to that language** before output — never force Chinese.
> 占位符如 `[收件人]` `[事由]` 为通用结构，跨语言保持一致。/ Placeholders like `[收件人]` are structural and stay consistent across languages.

# 行动项跟踪表

| 来源 | 事项 | 负责人 | 截止日 | 当前状态 | 风险/备注 |
|------|------|--------|--------|----------|----------|
| 纪要 1 | [动词 + 对象 + 交付物] | [姓名] | [YYYY-MM-DD] | 未开始 / 进行中 / 已阻塞 / 已完成 |  |
| 纪要 2 | [动词 + 对象 + 交付物] | [姓名] | [YYYY-MM-DD] | 未开始 / 进行中 / 已阻塞 / 已完成 |  |

状态说明：
- 未开始：已识别，尚未行动
- 进行中：已启动，有可见进展
- 已阻塞：因资源/依赖/决策停滞，需升级
- 已完成：已交付并通过验收

## 本周重点推进
- 高优先级 / 临近截止：
- 已阻塞需升级：

> 用法：提供多个会议纪要或零散待办，WorkBuddy 提取统一跟踪。建议调用 `xlsx` 技能生成可编辑表格，方便后续更新状态。

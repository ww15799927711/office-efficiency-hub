> **模板语言 / Template language**：本模板默认中文。当用户以英文（或其他语言）输入时，agent 应**把模板内容本地化为该语言**再输出，不强行用中文。
> This template is Chinese by default. When the user writes in English (or another language), the agent should **localize the content to that language** before output — never force Chinese.
> 占位符如 `[收件人]` `[事由]` 为通用结构，跨语言保持一致。/ Placeholders like `[收件人]` are structural and stay consistent across languages.

# 会议纪要到 PPT 大纲

**主题**：
**受众**：
**目标**：[汇报决策 / 同步进度 / 推动行动]

## 封面
- 标题：
- 副标题：
- 汇报人 / 日期：

## 目录页
1. 背景
2. 关键进展
3. 问题与风险
4. 决策与下一步
5. 所需支持

## 内容页

### 第 1 页：背景
- 一句话定位
- 2-3 个支撑要点

### 第 2 页：关键进展
- 数据/结果
- 与预期的对比

### 第 3 页：问题与风险
- 当前阻塞
- 潜在风险

### 第 4 页：决策与下一步
- 已达成决策
- 行动项（负责人 + 时间）

### 第 5 页：所需支持
- 需要决策/资源/协调的事项

## 结尾页
- 核心诉求 / 需要支持 / 确认项
- 联系方式

> 用法：WorkBuddy 根据纪要或素材生成此大纲，然后调用 `pptx` 技能生成实际幻灯片。每页只保留一个核心观点，避免文字堆砌。

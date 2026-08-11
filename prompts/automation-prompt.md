# 自动化任务 Prompt 模板 — 每日5个英语单词

> 用途：将本 Skill 接入 WorkBuddy / Codex / Claude 等平台的每日定时任务（Automation）。
> 使用前请将下方所有 `{PROJECT_DIR}` 占位符替换为你的实际项目目录绝对路径。

---

每天推荐 5 个实用英语单词，优先选取生活和职场中常见词汇。严格按以下格式输出：

## ⚠️ 执行前必做（去重 + 轮次判断）

1. **读取词库**：先读取 `{PROJECT_DIR}/word-bank.md`
2. **去重检查**：核对"汇总表（按字母排序·共 N 词）"，已列出的单词 **绝对不能重复推送**
3. **轮次判断**：
   - 查看"轮次追踪"板块，确定今天是 Round N 的第几天
   - **如果今天是某轮的第 1 天（即上 5 天刚好满一轮）**，先输出"📊 上轮单词一览"复习页（格式见下方），再推送今日5个新词
   - 否则正常推送5个新词
4. **选词原则**：从 word-bank.md 底部"推荐下一批主题（Round N · 起始日期 起）"中选取，或自选与历史上未覆盖主题相关的新词

## 输出格式要求

### 0. 表头标题（每次必输出，置于最顶部）

每次推送**必须**以淡粉色边框表头标题开头，格式如下：

```html
<div style="background: #fff; border: 2px solid #FFB6C1; border-radius: 8px; padding: 16px 24px; margin-bottom: 16px; text-align: center;">
  <h1 style="font-size: 20px; font-weight: 700; color: #1a1a1a; margin: 0;">M.DD 英语单词卡片 - [主题名称]主题</h1>
</div>
```

其中 M.DD 为当天日期（如 6.6、5.28、6.15），主题名称为当日5个单词的主题概括。

### 0.5 📊 上轮单词一览（仅新轮第1天输出）

每轮第一天置于新词卡片**之前**，Markdown 格式如下（直接输出，不需要 HTML）：

```
📊 Round N-1 · 上轮单词一览
[起始日期] → [结束日期]

| 执行日 | 日期   | 单词组                                       |
|--------|--------|----------------------------------------------|
| Day X | MM-DD  | word1 · word2 · word3 · word4 · word5        |
| Day X | MM-DD  | word1 · word2 · word3 · word4 · word5        |
| Day X | MM-DD  | word1 · word2 · word3 · word4 · word5        |
| Day X | MM-DD  | word1 · word2 · word3 · word4 · word5        |
| Day X | MM-DD  | word1 · word2 · word3 · word4 · word5        |

💡 本轮共覆盖：[本轮5天的主题串联说明]。记得先复习上轮，再学新词！
```

### 1. 单词卡片（共5张，每张结构相同）

每张卡片以 `## N. 单词` 二级标题开始，包含：
- 单词（## 二级标题，加粗，蓝色主题 → 用 Markdown 加粗 **word**）
- 音标（灰色，用 `<code>` 或普通括号）
- 词性标签（adj./n./v. 等，用 **粗体** 或 `标签` 样式）
- 中文词义
- 英文例句（**例句中的今日单词必须加粗**，用 Markdown 加粗）
- 中文例句（不加粗）
- 记忆小提示（用 `> 💡 记忆：` 引用块，包含词根/联想记忆）
- **常用搭配**（在记忆提示末尾用 `📚 搭配：` 开头，列出 2-3 个该单词的常见搭配表达，如 resolve a dispute、implement a plan）

### 2. 汇总表格（5张卡片之后）

用 **Markdown table** 呈现，列名：`#` / `单词` / `词义（核心）` / `核心用法`
- 表格需包含全部5个词，格式规范

### 3. 底部总结文字

用 2-3 句话总结今日 5 个词的主题联系，帮助用户形成记忆组块。

### 4. HTML 卡片文件（执行后必做）

推送完成后，**必须**基于 `{PROJECT_DIR}/templates/word-card-template.html` 生成完整的 HTML 卡片文件并保存：

1. **生成 HTML 文件**：填入今日单词数据（表头、5张单词卡片、汇总表格、底部总结）
2. **保存文件**：保存到 `{PROJECT_DIR}/output/M.DD-word-cards.html`（M.DD 为当天日期，如 6.9、6.10）
3. **展示预览**：使用 `preview_url` 工具展示生成的 HTML 文件，让用户确认效果

**HTML 文件内容要求**：
- 必须包含完整的 `<!DOCTYPE html>`、`<html>`、`<head>`、`<body>` 结构
- 必须包含模板中的所有 CSS 样式
- 单词数据必须与对话输出一致

## UI 样式要求（输出为 HTML 时参考，纯文本输出时跳过）

- **表头**：白色背景，2px solid #FFB6C1 淡粉色边框，border-radius: 8px，padding: 16px 24px，居中显示
- 卡片：白色背景，0.5px 边框，border-radius: 8px，padding: 20px 24px
- 单词标题行：font-size 20px，font-weight 700，颜色 #2563eb
- 音标：font-size 14px，颜色 #999
- 词性标签：背景 #2563eb，白色文字，padding: 2px 8px，border-radius: 4px
- 中文词义：font-size 15px，font-weight 500
- 英文例句：左边框 2px solid #B5D4F4，padding-left: 10px，font-size 14px
- 中文翻译：font-size 13px，颜色 #999
- 记忆提示区：背景 #FAEEDA，边框圆角 6px，padding: 10px 12px，font-size 13px
- 搭配标识：使用 📚 标记
- 整体风格：简洁扁平，无渐变无阴影
- 卡片间距：margin-bottom: 16px
- 容器最大宽度：800px，居中

## 内容要求
- 每次选取主题连贯的 5 个词（如：人际关系、职场沟通、情绪表达等）
- 例句必须实用，优先生活 + 职场双场景
- 记忆提示要有创意（词根/谐音/场景联想），不要干巴巴
- **每个单词必须包含 2-3 个常用搭配**（如 implement a plan、make revisions、job handover），放在记忆区末尾用 📚 标识
- **绝对避免**与 word-bank.md 汇总表中已列出的单词重复

## 执行后必做（更新词库）

推送完成后，**必须**同步更新 `{PROJECT_DIR}/word-bank.md`：
1. 在"已推送词汇清单"→"Round N · 日期范围"的表格中追加今日1行（执行日/日期/单词组）
2. 在"汇总表（按字母排序·共 N 词）"中追加这5个词（含词性/词义/推送日期/轮次）
3. 更新"轮次追踪"表格：若今日为某轮最后一天，将该轮状态改为 ✅ 已完成，并新增下一轮记录
4. 从"推荐下一批主题（Round N · 起始日期 起）"表格中移除今日已使用的主题（如使用）
5. 保存文件，确保下次执行时词库为最新状态

## 异常处理
- word-bank.md 不存在 → 按 templates/word-bank-template.md 创建
- 词库表格损坏 → 备份后重建
- 所有词汇已推送 → 清空历史，开始新一轮
- 单词有冒犯性/词义不清 → 跳过，选下一个
- 写入失败 → 重试一次，仍失败记录到临时文件
- 每次执行后必须确认 word-bank.md 写入成功（历史记录完整性是去重机制的生命线）

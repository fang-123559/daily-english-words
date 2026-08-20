# 每日六词自动化任务

显式调用 `$daily-english-words`，在当前项目根目录完成一次每日六词生成。

## 执行要求

1. 严格读取并遵循 `.agents/skills/daily-english-words/SKILL.md`。
2. 除非用户明确指定旧风格模板，否则使用默认六词 V3 模式。
3. 读取 `word-bank.md`，确保今日 6 个单词与全部历史记录不重复。
4. 生成主题连贯的 6 个实用词，优先采用 `2 adj. + 2 n. + 2 v.`。
5. 使用 `.agents/skills/daily-english-words/templates/word-card-template.html` 的结构与配色。
6. 保存完整 HTML 到 `output/YYYY-MM-DD-daily-english.html`。
7. 更新并复查 `word-bank.md`。
8. 最终只汇报日期、主题、六个单词、输出文件路径和词库更新结果；失败时明确指出失败步骤，不静默降级。

## 五词兼容模式

- 用户明确指定 `templates/styles/` 下的旧风格时，切换为五词模式，生成 5 个词并保持该旧模板结构。
- 不修改或重排 `templates/styles/` 下的既有模板，也不把六词数据硬塞进五词模板。

## 默认六词模式不得改变

- 每日数量固定为 6 个。
- 桌面端每行 2 张卡片，680px 及以下单列。
- 卡片编号使用 `WORD_01–WORD_06`。
- 每张卡片同时包含“记忆”和“使用辨析／使用提示”。
- 顶栏日期、主动回忆、折叠六词汇总和学习路径必须保留。
- 配色保持米白、白色、橄榄绿和柔和浅灰，不改成蓝色或粉色主题。

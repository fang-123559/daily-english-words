# 每日5个英语单词 Daily English Words 📚

一个**开箱即用的 Skill 模板**：让 AI 每天推荐 5 个主题连贯的实用英语单词，输出**结构化单词卡片 + 汇总表格 + 精美 HTML 卡片文件**，并自动去重、按轮次复习、记录词库。

> 每天 5 个词 · 主题连贯 · 越学越顺

---

## ✨ 特性

- 📚 **每日 5 词**：每次推荐 5 个主题连贯的实用单词（生活 + 职场双场景）
- 🎴 **结构化卡片**：单词 / 音标 / 词性 / 词义 / 例句 / 记忆提示 / 常用搭配，一应俱全
- 📄 **HTML 卡片文件**：自动生成精美 HTML，可直接分享或用于小红书等平台
- 🔄 **轮次复习机制**：每轮结束自动生成「上轮单词一览」复习页，温故知新
- 🛡️ **自动去重**：基于 `word-bank.md` 词库汇总表，绝不重复推荐
- 🛡️ **工程化设计**：内置失败模式编码、异常处理表、反例黑名单（详见 SKILL.md）
- ⚙️ **可接入自动化**：可配置为每日定时任务自动执行

## 🖼️ 效果预览

**6.25 跨文化沟通主题**（diverse / inclusive / cultural / global / multilingual）：

<p align="center">
  <img src="examples/2026-06-25-cross-cultural-communication.png" width="380"/>
</p>

> 📄 完整 HTML 示例见 [examples/](examples/)：

| 示例 | 主题 | 单词 | 推送日期 |
|------|------|------|----------|
| [2026-06-23](examples/2026-06-23-leadership.html) | 领导力 | inspire · empower · mentor · motivate · vision | 2026-06-23 |
| [2026-06-24](examples/2026-06-24-innovative-thinking.html) | 创新思维 | creative · brainstorm · prototype · iterate · experiment | 2026-06-24 |
| [2026-06-25](examples/2026-06-25-cross-cultural-communication.html) | 跨文化沟通 | diverse · inclusive · cultural · global · multilingual | 2026-06-25 |

## 📦 安装方法

### 方式一：直接把链接丢给 AI Agent（小白最推荐 🌟）

**什么都不用自己操作**，只需把下面这段话复制给你的 AI 助手（WorkBuddy / Codex / Claude 等），让它自己去下载、安装，再教你怎么用：

> 请帮我把这个 GitHub 仓库的 Skill 安装好：
> 仓库：https://github.com/fang-123559/daily-english-words
> 请先下载（git clone 或下载 ZIP），把 `daily-english-words` 文件夹放到我的 skills 目录
> （WorkBuddy: `~/.workbuddy/skills/`，Codex: `~/.codex/skills/`，Claude: `~/.claude/skills/`），
> 确认 `SKILL.md` 在文件夹根目录，然后告诉我怎么用它。

也可以直接让 Agent 执行下面的命令完成下载：

```bash
git clone https://github.com/fang-123559/daily-english-words.git
# 然后按提示把 daily-english-words 文件夹复制到你对应平台的 skills 目录
```

### 方式二：手动下载（推荐新手）

1. 点击右上角 **Code → Download ZIP** 下载并解压
2. 将解压后的文件夹放入你的 Skill 目录：
   - **WorkBuddy**：`~/.workbuddy/skills/`
   - **Codex**：`~/.codex/skills/`
   - **Claude**：`~/.claude/skills/`
   - 其他支持 Agent Skills 的平台：放入对应 skills 目录
3. 确保文件夹名为 `daily-english-words`，且 `SKILL.md` 在文件夹根目录

### 方式三：Git 克隆

```bash
git clone https://github.com/fang-123559/daily-english-words.git
# 然后将整个文件夹复制到 skills 目录
```

## 🚀 使用方式

### 方式一：对话中直接触发

安装完成后，在 AI 对话中输入任意触发词，即可生成今日单词卡片：

> "每日英语单词"、"推荐5个英语单词"、"今天学什么单词"

### 方式二：接入自动化定时推送（推荐）

在 WorkBuddy / Codex / Claude 等平台创建一个每日定时任务，prompt 可参考 [prompts/automation-prompt.md](prompts/automation-prompt.md)：

```text
每天推荐 5 个英语单词，严格按 SKILL.md 的 daily-english-words 模板执行：
读取 word-bank.md 词库去重 → 判断轮次 → 选 5 个主题连贯的新词 → 输出卡片+表格+HTML → 更新词库
```

首次使用请复制 [templates/word-bank-template.md](templates/word-bank-template.md) 为项目根目录下的 `word-bank.md`。

## 🗂️ 项目结构

```
daily-english-words/
├── SKILL.md                      # Skill 核心定义（执行流程 + 模板规范 + 异常处理）
├── README.md                     # 本文件
├── LICENSE                       # MIT 许可证
├── prompts/
│   └── automation-prompt.md      # 自动化定时任务的 prompt 模板
├── templates/
│   ├── word-bank-template.md     # word-bank.md 词库模板（去重用）
│   └── word-card-template.html   # HTML 卡片模板
└── examples/                     # 完整输出示例（HTML 卡片文件）
```

## ⚙️ 自定义

- **改配色**：修改 `templates/word-card-template.html` 中 CSS 的 `#2563eb`（主色）、`#FFB6C1`（表头边框色）
- **改推送风格**：调整「单词卡片」部分的模板结构
- **改触发场景**：修改 SKILL.md frontmatter 中的 `description` 触发词

## 📜 License

[MIT](LICENSE) © fang-123559

---

<p align="center"><b>每天 5 个词 · 让英语融入生活</b> 🇬🇧</p>

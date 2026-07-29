# 🎙️ 语音 → 文章

> **5 分钟录音。发布一篇 SEO 文章。花费 $0.12。**

---

<br>

### 痛点

你的网站空空如也。不是因为你无话可说——而是因为写一篇文章要花 5 个小时，而你根本没那个时间。

### 解决方案

打开 Telegram。点击录音。像跟朋友聊天一样，把你的想法说出来。

AI 转写 → 研究热门关键词 → **用你的语气**写出文章 → 部署到你的网站，附带结构化数据（Schema）、元标签、交叉链接和站点地图。

```
📱 语音备忘录  →  🔍 语义分析  →  ✍️ 文章  →  🚀 网站上线
      5 分钟           自动             自动            自动
```

不需要 Ahrefs。不需要 Semrush。不需要面对空白页面。只需要你和你的手机。

---

## 它能做什么

1. **你发送语音消息** → Telegram 机器人通过 Whisper 进行语音转文字
2. **AI 提取结构** → 论点、章节、常见问题（FAQ）、关键词
3. **语义研究** → 使用 Yandex Wordstat（俄罗斯版 Google Keyword Planner）或 Google Suggest（英语）挖掘热门话题
4. **AI 撰写文章** → DeepSeek（或 Claude/GPT）— SEO 优化，人类可读
5. **自动部署** → FTP/SCP 上传到你的网站 + GitHub Markdown 备份
6. **结构化数据标记** → 文章 + FAQPage JSON-LD，提升 AI 搜索可见性（AEO）

专为 **Hermes Agent** 构建。同时可移植到 Claude Code、Codex CLI、Cursor 或任何 LLM 代理。

---

## 为什么做这个

写博客文章很痛苦。编辑 AI 生成的废话更痛苦。这套流程保留了**你的语气**——俚语、个性、直率——同时处理无聊的部分：语义分析、文章结构、SEO 标签、部署。

**独立创业者的内容飞轮：**
```
语音备忘录（5 分钟）→ 发布 SEO 文章（永久有效）
```

不需要仪表盘。不需要内容日历。只管聊你懂的东西。

---

## 对比传统方式

| 传统方式 | 本工具 |
|-------------|-----------|
| 打开 Ahrefs → 关键词研究（1 小时） | AI 自动进行语义研究 |
| 在 Notion 中列大纲（30 分钟） | AI 从你的语音中提取结构 |
| 写草稿（2 小时） | 你已经说完了——那就是草稿 |
| 编辑、反复修改、盯着屏幕（1 小时） | AI 用你的语气撰写，而非企业腔调 |
| 手动添加元标签、Schema、OG（30 分钟） | Article + FAQPage Schema 自动生成 |
| FTP/SCP 上传、站点地图、交叉链接（30 分钟） | 自动部署 + 站点地图 + 交叉链接 |
| **总计：5+ 小时** | **总计：5 分钟录音** |

**本工具为独立创业者替代的工具：**
- **Ahrefs / Semrush** — 关键词研究。由 Wordstat（俄语）+ Google Suggest（英语）+ AI 聚类替代。
- **Jasper / Copy.ai / Writesonic** — AI 文案写作。由带有你的语气提示词的 DeepSeek 替代。
- **SurferSEO / Clearscope** — 内容优化。由语义聚类注入 Article Schema 替代。
- **WordPress / Ghost / Webflow** — 内容管理系统（CMS）。由通过 SCP/FTP 部署的静态 HTML 替代。
- **Yoast / RankMath** — 页面内 SEO。由自动生成的元标签、hreflang、Schema、canonical 替代。
- **人工文案写手** — 每篇文章 $200-500。由 $0.12 的 API 调用替代。

你仍然需要大脑。你仍然需要专业知识。但你不再需要 6 个工具和一个下午来发布一篇文章。

---

## 适用人群

- **独立创业者** — 需要内容但讨厌写作
- **独立开发者** — 推出产品但零营销团队
- **咨询师/代理机构** — 习惯边想边说，希望把想法发布出去
- **非写作者** — 拥有领域专长和一部手机

---

## 技术栈与成本

| 组件 | 功能 | 成本 |
|-----------|-------------|------|
| **Telegram 机器人** | 接收语音消息 | 免费 |
| **Whisper（OpenAI）** | 语音转文字 | $0.006/分钟（约 $0.10/篇） |
| **DeepSeek API** | 文章生成 + 语义分析 | 约 $0.015/篇 |
| **Yandex Wordstat** | 俄语关键词研究 | 约 $0.005/100 次查询 |
| **你的服务器** | 托管发布后的 HTML | 按你的服务器费用 |

**约 $0.12 每篇发布文章。** 比一杯咖啡还便宜。比大多数广告投放的 ROI 更好。

---

## 设置（5 分钟）

### 1. 创建 Telegram 机器人
```
对话 @BotFather → /newbot → 获取 token
```

### 2. 获取 API 密钥
- **OpenAI**（Whisper）：https://platform.openai.com/api-keys
- **DeepSeek**：https://platform.deepseek.com/api_keys
- **Yandex Wordstat**（可选，仅俄语）：https://oauth.yandex.ru

### 3. 配置你的代理

**Hermes Agent：**
```bash
# 添加技能
cp SKILL.md ~/.hermes/profiles/marketing/skills/

# 设置环境变量
export OPENAI_API_KEY="sk-..."
export DEEPSEEK_API_KEY="sk-..."
export TELEGRAM_BOT_TOKEN="123:abc"
```

**Claude Code / Codex / Cursor：**
```bash
# 将 PROMPT.md 复制到你的代理的系统提示词或 .cursorrules 中
# 将 API 密钥添加到你的环境中
```

### 4. 指向你的网站
编辑 `SKILL.md` → 更新部署部分，填入你的 FTP/SCP 凭据和路径。

### 5. 开始口述
向你的机器人发送一条语音消息。代理会接收、转写、结构化、撰写并部署。

---

## 工作流程（可视化）

```
📱 Telegram 语音消息
        ↓
🗣️ OpenAI Whisper → 原始转录文本
        ↓
🧠 AI 提取：论点、章节、FAQ、关键词
        ↓
🔍 Yandex Wordstat（俄语）/ Google Suggest（英语）→ 热门语义
        ↓
✍️ DeepSeek 撰写：带 Article + FAQPage Schema 的 HTML 文章
        ↓
🚀 部署：FTP/SCP 到你的网站 + GitHub Markdown
        ↓
📊 SEO：站点地图更新、交叉链接、搜索引擎通知
```

---

## 真实数据

来自我的生产流水线（axelfreeman.com + axelfreeman.ru）：

- **83 个已发布的问答页面**（44 个俄语 + 39 个英语）
- **每月约 10 万次搜索展示**，覆盖两种语言
- **每页 4-6 个 FAQ 条目**，附带 FAQPage Schema
- **收到语音备忘录后 <2 分钟**文章即发布

---

## 语义引擎

这不是"AI 帮我写了一篇博客"。这是：

- **热门话题检测** — 通过 Wordstat 动态数据发现正在增长的话题
- **聚类分析** — 按意图而非仅仅按搜索量对关键词进行分组
- **精确匹配过滤** — 广泛匹配的数字会撒谎，精确匹配才能揭示真相
- **跨语言** — 俄语通过 Yandex，英语通过 Google Suggest

以"AI 文案写作"（俄语市场）的语义聚类为例：

| 聚类 | 搜索量 | 热门短语 |
|---------|--------|------------|
| AI 文本生成 | 330K/月 | нейросеть текст |
| AI 写作 | 36K/月 | ии для написания текстов |
| 语音 → 文字 | 70K/月 | аудио в текст |
| SEO 文案 | 170/月 | seo текст сайт |
| 内容创作 | 60K/月 | создание контента |

完整语义数据：`semantics/` 目录。

---

## 示例

**输入：** 一段 5 分钟的语音备忘录，讨论为什么 Telegram 是 AI 代理的最佳平台。

**输出：** [axelfreeman.com 上的已发布文章](https://axelfreeman.com/blog/ai-agents-on-telegram.html)，包含：
- SEO 标题 + 元描述
- 8 个 H2 章节，附带要点列表
- 2 个卡片区块（关键洞察 + 行动号召）
- 6 个 FAQ，附带匹配的 JSON-LD Schema
- 指向俄语版本的 hreflang 交叉链接
- Yandex Metrika 追踪

完整的前后对比见 `examples/`。

---

## 可移植性

| 代理 | 使用方式 |
|-------|-----------|
| **Hermes Agent** | 将 `SKILL.md` 放入技能目录 |
| **Claude Code** | 将 `PROMPT.md` 粘贴到 CLAUDE.md 中 |
| **Codex CLI** | 复制到 `.codex.md` 或作为系统提示词传入 |
| **Cursor** | 添加到 `.cursorrules` |
| **任意 LLM** | `PROMPT.md` 可直接作为独立的系统提示词使用 |

---

## 文件结构

```
voice-to-article/
├── README.md              ← 你在这里
├── SKILL.md               ← Hermes Agent 技能（完整流水线）
├── PROMPT.md              ← 适用于任意 LLM 代理的通用系统提示词
├── SETUP.md               ← 详细设置：机器人、密钥、部署目标
├── semantics/
│   ├── ru-clusters.json   ← 俄语关键词聚类（Wordstat）
│   └── en-suggestions.json← 英语关键词建议（Google Suggest）
├── examples/
│   ├── voice-memo-raw.txt ← 真实语音备忘录的原始转录
│   ├── article-ru.html    ← 最终发布的俄语文章
│   └── article-en.html    ← 最终发布的英语文章
└── .github/
    └── FUNDING.yml
```

---

## 延伸阅读

- [为什么 Claude 不适合做营销](https://github.com/axelfreeman/blog/blob/main/posts/claude-sucks-for-marketing.md) — 为什么我选择 DeepSeek 来生成内容
- [Yandex Wordstat 指南](https://github.com/axelfreeman/yandex-wordstat-guide) — 俄语关键词研究的完整 API 参考
- [不扯淡的 AI 营销](https://axelfreeman.com) — 我的博客

---

## 许可证

MIT — 使用它、修改它、发布它。如果这个工具帮你节省了时间，[请我喝杯咖啡](https://t.me/axelfreeman)。

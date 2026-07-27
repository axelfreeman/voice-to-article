# 🎙️ Voice → Article: AI SEO Copywriting Pipeline

**Dictate blog posts in Telegram. Get SEO-optimized articles deployed to your site.**

You talk. AI listens, researches semantics, writes, and deploys. The fastest way for a solopreneur to produce SEO content — voice memos in, published articles out.

---

## What It Does

1. **You send voice notes** → Telegram bot transcribes via Whisper
2. **AI extracts structure** → thesis, sections, FAQ, keywords
3. **Semantic research** → Yandex Wordstat (RU) or Google Suggest (EN) for trending topics
4. **AI writes the article** → DeepSeek (or Claude/GPT) — SEO-optimized, human-readable
5. **Auto-deploy** → FTP/SCP to your site + GitHub markdown backup
6. **Schema markup** → Article + FAQPage JSON-LD for AI search visibility (AEO)

Built for **Hermes Agent**. Portable to Claude Code, Codex CLI, Cursor, or any LLM agent.

---

## Why This Exists

Writing blog posts sucks. Editing AI-generated fluff sucks more. This pipeline preserves **your voice** — slang, personality, directness — while handling the boring parts: semantics, structure, SEO tags, deployment.

**The solopreneur content flywheel:**
```
Voice memo (5 min) → Published SEO article (forever)
```

No dashboards. No content calendars. Just talk about what you know.

---

## Who Is This For

- **Solopreneurs** who need content but hate writing
- **Indie hackers** launching products with zero marketing team
- **Consultants/agencies** who think out loud and want that published
- **Non-writers** with domain expertise and a phone

---

## Tech Stack & Cost

| Component | What It Does | Cost |
|-----------|-------------|------|
| **Telegram Bot** | Receives voice messages | Free |
| **Whisper (OpenAI)** | Speech-to-text | $0.006/min (~$0.10/article) |
| **DeepSeek API** | Article generation + semantics | ~$0.015/article |
| **Yandex Wordstat** | RU keyword research | ~$0.005 per 100 queries |
| **Your server** | Host the published HTML | Whatever you pay |

**~$0.12 per published article.** Cheaper than a coffee. Better ROI than most ad spend.

---

## Setup (5 minutes)

### 1. Create a Telegram Bot
```
Talk to @BotFather → /newbot → get token
```

### 2. Get API Keys
- **OpenAI** (Whisper): https://platform.openai.com/api-keys
- **DeepSeek**: https://platform.deepseek.com/api_keys
- **Yandex Wordstat** (optional, RU only): https://oauth.yandex.ru

### 3. Configure Your Agent

**Hermes Agent:**
```bash
# Add the skill
cp SKILL.md ~/.hermes/profiles/marketing/skills/

# Set env vars
export OPENAI_API_KEY="sk-..."
export DEEPSEEK_API_KEY="sk-..."
export TELEGRAM_BOT_TOKEN="123:abc"
```

**Claude Code / Codex / Cursor:**
```bash
# Copy PROMPT.md into your agent's system prompt or .cursorrules
# Add API keys to your environment
```

### 4. Point It at Your Site
Edit `SKILL.md` → update deploy section with your FTP/SCP credentials and paths.

### 5. Start Dictating
Send a voice message to your bot. The agent picks it up, transcribes, structures, writes, and deploys.

---

## The Workflow (Visual)

```
📱 Telegram Voice Note
        ↓
🗣️ OpenAI Whisper → Raw transcript
        ↓
🧠 AI extracts: thesis, sections, FAQ, keywords
        ↓
🔍 Yandex Wordstat (RU) / Google Suggest (EN) → Trending semantics
        ↓
✍️ DeepSeek writes: HTML article with Article+FAQPage Schema
        ↓
🚀 Deploy: FTP/SCP to your site + GitHub markdown
        ↓
📊 SEO: sitemap update, cross-links, search engine ping
```

---

## Real Numbers

From my production pipeline (axelfreeman.com + axelfreeman.ru):

- **83 published Q&A pages** (44 RU + 39 EN)
- **~100K monthly search impressions** across both languages
- **4-6 FAQ items per page** with FAQPage Schema
- **Article published in <2 minutes** after voice memo received

---

## The Semantic Engine

This isn't "AI wrote me a blog post." This is:

- **Trending topic detection** — Wordstat dynamics to find what's growing
- **Cluster analysis** — group keywords by intent, not just volume
- **Exact match filtering** — broad numbers lie, exact match tells the truth
- **Cross-language** — RU via Yandex, EN via Google Suggest

Example semantic clusters for "AI copywriting" (RU market):

| Cluster | Volume | Top Phrase |
|---------|--------|------------|
| AI text generation | 330K/mo | нейросеть текст |
| AI for writing | 36K/mo | ии для написания текстов |
| Voice → text | 70K/mo | аудио в текст |
| SEO copywriting | 170/mo | seo текст сайт |
| Content creation | 60K/mo | создание контента |

Full semantic data: `semantics/` directory.

---

## Example

**Input:** 5-minute voice memo about why Telegram is the best platform for AI agents.

**Output:** [Published article on axelfreeman.com](https://axelfreeman.com/blog/ai-agents-on-telegram.html) with:
- SEO title + meta description
- 8 H2 sections with bullet points
- 2 card blocks (key insight + CTA)
- 6 FAQ with matching JSON-LD Schema
- hreflang cross-link to RU version
- Yandex Metrika tracking

See `examples/` for the full before/after.

---

## Portability

| Agent | How to Use |
|-------|-----------|
| **Hermes Agent** | Drop `SKILL.md` into skills directory |
| **Claude Code** | Paste `PROMPT.md` into CLAUDE.md |
| **Codex CLI** | Copy to `.codex.md` or pass as system prompt |
| **Cursor** | Add to `.cursorrules` |
| **Any LLM** | `PROMPT.md` works as a standalone system prompt |

---

## Files

```
voice-to-article/
├── README.md              ← You are here
├── SKILL.md               ← Hermes Agent skill (full pipeline)
├── PROMPT.md              ← Universal system prompt for any LLM agent
├── SETUP.md               ← Detailed setup: bots, keys, deploy targets
├── semantics/
│   ├── ru-clusters.json   ← RU keyword clusters (Wordstat)
│   └── en-suggestions.json← EN keyword suggestions (Google Suggest)
├── examples/
│   ├── voice-memo-raw.txt ← Raw transcript of a real voice memo
│   ├── article-ru.html    ← Final published RU article
│   └── article-en.html    ← Final published EN article
└── .github/
    └── FUNDING.yml
```

---

## Read Also

- [Why Claude Sucks for Marketing](https://github.com/axelfreeman/blog/blob/main/posts/claude-sucks-for-marketing.md) — why I use DeepSeek for content
- [Yandex Wordstat Guide](https://github.com/axelfreeman/yandex-wordstat-guide) — full API reference for RU keyword research
- [AI Marketing Without Bullshit](https://axelfreeman.com) — my blog

---

## License

MIT — use it, remix it, ship it. If this saves you time, [buy me a coffee](https://t.me/axelfreeman).

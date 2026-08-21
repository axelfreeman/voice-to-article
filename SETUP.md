# Setup Guide: Voice → Article Pipeline

Step-by-step. No fluff.

---

## Prerequisites

- A Telegram account
- A server with nginx/Apache (or any static hosting)
- $5-10 on API credits (lasts months)

---

## Step 1: Telegram Bot

1. Open Telegram → search `@BotFather`
2. Send `/newbot`
3. Name it (e.g. "My Content Bot")
4. Get the token (looks like `123456:ABC-DEF1234gh...`)
5. Save it: `export TELEGRAM_BOT_TOKEN="123456:ABC..."`

**Important:** The bot must be able to receive voice messages. No special setup needed — Telegram handles voice natively.

---

## Step 2: API Keys

### OpenAI (Whisper — speech to text)
1. Go to https://platform.openai.com/api-keys
2. Create new secret key
3. `export OPENAI_API_KEY="sk-..."`

**Cost:** $0.006 per minute of audio. A 5-minute voice memo = $0.03.

### DeepSeek (article generation)
1. Go to https://platform.deepseek.com/api_keys
2. Create API key
3. `export DEEPSEEK_API_KEY="sk-..."`

**Cost:** ~$0.015 per article. DeepSeek is ~15x cheaper than GPT-4 for comparable quality on content tasks. Claude is even more expensive — use DeepSeek.

### Google Suggest + Trends (keyword research — free, no key)
No setup needed. The pipeline calls `suggestqueries.google.com` (autocomplete) and `pytrends` (Google Trends) directly — zero API keys, zero cost.

**Cost:** $0.

---

## Step 3: Deploy Target

### Option A: Your own server (SCP)
```bash
export DEPLOY_HOST="your-server.com"
export DEPLOY_USER="root"
export DEPLOY_PATH="/var/www/yoursite.com/blog/"
```

The agent will:
1. Write HTML locally
2. `scp` to your server
3. `chown www-data:www-data` (for nginx)
4. Verify: `curl -sI https://yoursite.com/blog/article-slug.html`

### Option B: FTP (shared hosting)
```bash
export FTP_HOST="ftp.yourhost.com"
export FTP_USER="username"
export FTP_PASS="password"
export FTP_PATH="/public_html/"  # web root on FTP
```

### Option C: GitHub Pages / static hosting
If you just want markdown on GitHub:
```bash
export GITHUB_REPO="yourname/blog"
```
The agent commits markdown files. No HTML deploy step.

---

## Step 4: Install the Skill

### Hermes Agent
```bash
# Copy to your profile's skills directory
cp SKILL.md ~/.hermes/profiles/<your-profile>/skills/voice-to-article.md

# Or symlink for auto-updates
ln -s $(pwd)/SKILL.md ~/.hermes/profiles/<your-profile>/skills/voice-to-article.md
```

### Claude Code
```bash
# Append to CLAUDE.md
cat PROMPT.md >> CLAUDE.md
```

### Codex CLI
```bash
cp PROMPT.md .codex.md
```

### Cursor
```bash
cp PROMPT.md .cursorrules
```

---

## Step 5: Test It

1. Send a voice message to your Telegram bot: "Testing the pipeline. This is a test article about why AI agents need better onboarding."
2. The agent should:
   - Transcribe the voice memo
   - Post a summary back
   - Research semantics (Google Suggest / Trends)
   - Generate HTML with Article+FAQPage Schema
   - Deploy to your server
3. Verify: open the URL in your browser

---

## Step 6: Customize

### Change the AI model
In `SKILL.md` or `PROMPT.md`, replace `deepseek-chat` with:
- `gpt-4o` — better writing, 15x more expensive
- `claude-sonnet-4-20250514` — good but $15/M tokens (vs DeepSeek's $0.28)
- `gemini-2.5-pro` — Google's latest, competitive pricing

### Add your own design system
Edit the HTML template in `PROMPT.md` → replace fonts, colors, layout.

### Add more semantic sources
- **Ahrefs/Semrush API** — keyword volumes
- **Google Keyword Planner** — via Ads API
- **DataForSEO** — structured SERP data

---

## Troubleshooting

| Problem | Likely Fix |
|---------|-----------|
| Telegram bot doesn't respond | Check token, bot must be started with `/start` |
| Whisper transcription empty | Voice message too short (<1s) or unsupported format |
| Article sounds like ChatGPT | Model is over-editing. Add "preserve raw voice" to prompt |
| Deploy 403 Forbidden | `chown www-data:www-data` on the uploaded file |
| Google Suggest returns few results | Phrase too niche. Use broader seed keywords |
| Google Trends rate-limited | HTTP 429 — slow down, add backoff |
| FAQPage Schema mismatch | Visible FAQ text ≠ JSON-LD text. They must be identical |
| FTP uploads to wrong directory | FTP root ≠ web root. Check `FTP_PATH` |

---

## Cost Estimate (Monthly)

For 10 articles/month:

| Item | Cost |
|------|------|
| Whisper (50 min audio) | $0.30 |
| DeepSeek (10 generations) | $0.15 |
| Keyword research (Google Suggest/Trends) | $0 |
| Server/hosting | $5-20 |
| **Total** | **~$5-20/month** |

vs. hiring a copywriter: $500-2000/month. 100x cheaper.

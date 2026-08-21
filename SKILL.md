---
name: voice-to-article
description: |
  Voice memo → SEO article pipeline. When the user sends voice notes to publish an article.
  Covers: voice transcription → structure extraction → semantic research → HTML generation
  → deploy with Article+FAQPage Schema.
  Triggers: voice notes, "dictate an article", "turn this voice memo into an article", voice-to-article.
version: 2.2.0
author: Axel Freeman
license: MIT
metadata:
  hermes:
    tags: [voice, article, seo, copywriting, telegram, content, publishing]
    required_env: [OPENAI_API_KEY, DEEPSEEK_API_KEY, TELEGRAM_BOT_TOKEN]
    optional_env: [DEPLOY_HOST, FTP_HOST]
---

# Voice → Article Pipeline

Turn Telegram voice memos into published SEO articles. The user dictates thoughts — you handle everything else.

## Workflow

### Phase 1: Receive & Transcribe

1. Voice memo arrives via Telegram → transcribe with OpenAI Whisper (exact call and key in SETUP.md).
2. Save RAW transcript (slang, profanity, repetitions — ALL of it).
3. Post bullet-point summary back to user as outline scaffold.

### Phase 2: Extract Structure

From raw transcript, identify:
- **Core thesis** — one sentence
- **Sections** — each logical chunk = one H2 (6-10 total)
- **Supporting points** — claims, examples, data, CTAs
- **FAQ candidates** — 4-6 questions the article raises

### Phase 3: Semantic Research

Query **Google Suggest** for topic angles and related queries — free, no API key. Works for any language (set `hl=` accordingly). For trending topics, use **Google Trends** (pytrends, also free).

Collect 6-10 target keywords for Article Schema. Prioritize exact match, growing topics.

### Phase 4: Write HTML

Generate HTML with DeepSeek API. **Critical: preserve author's voice.** Do NOT rewrite into corporate-speak.

**HTML requirements:**
- Article + FAQPage JSON-LD Schema
- TLDR block: bold opener + 2-3 sentence summary
- 6-10 H2 sections with mix of <p>, <ul>, <ol>
- 2-4 card blocks (block-text class) for insights/CTAs/warnings
- 4-6 FAQ Q&A — must match JSON-LD EXACTLY
- Design: Merriweather + Ubuntu, H2 weight:500 margin:48px 0 8px, accent #2563eb

### Phase 5: Deploy

Push the finished HTML to the deploy target (SCP or FTP — exact host and credentials live in SETUP.md, never hardcoded).

### Phase 6: Post-Deploy

1. Add URL to sitemap.xml
2. Add promo card to homepage
3. Cross-link from existing articles (Read next blocks)
4. Create GitHub markdown backup → push to blog repo
5. Ping search engines (Google + Bing)
6. Verify the deployed URL returns HTTP 200

## Verification

- [ ] Deployed URL returns HTTP 200
- [ ] Article + FAQPage Schema present (grep for JSON-LD)
- [ ] FAQPage visible text matches JSON-LD (grep both, diff)
- [ ] Sitemap updated
- [ ] Homepage card live
- [ ] Cross-links added to existing articles

## Pitfalls

1. **FAQPage mismatch:** visible FAQ text ≠ JSON-LD text → SEO penalty
2. **FTP path:** FTP root ≠ web root. Verify the actual served directory
3. **chown after SCP:** files created as root → nginx returns 403
4. **Voice preservation:** Don't over-edit. Slang, directness, profanity stay
5. **Google Trends rate limit:** pytrends returns HTTP 429 if polled too fast — add backoff between requests
6. **Wildcard deploy:** the blog uses a /blog/ subdirectory (varies by setup)

## Dependencies

- `OPENAI_API_KEY` — Whisper transcription
- `DEEPSEEK_API_KEY` — Article generation
- `TELEGRAM_BOT_TOKEN` — Receive voice messages
- Server with SSH or FTP access — deploy target

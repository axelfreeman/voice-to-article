---
name: voice-to-article
description: |
  Voice memo → SEO article pipeline. When the user sends voice notes to publish an article.
  Covers: voice transcription → structure extraction → semantic research → HTML generation
  → dual-language deploy with Article+FAQPage Schema.
  Triggers: голосовухи, voice notes, "запиши статью", "надиктуй", voice-to-article.
version: 2.0.0
author: Axel Freeman
license: MIT
metadata:
  hermes:
    tags: [voice, article, seo, copywriting, telegram, content, publishing]
    required_env: [OPENAI_API_KEY, DEEPSEEK_API_KEY, TELEGRAM_BOT_TOKEN]
    optional_env: [WORDSTAT_API_KEY, WORDSTAT_FOLDER_ID, DEPLOY_HOST, FTP_HOST]
---

# Voice → Article Pipeline

Turn Telegram voice memos into published SEO articles. The user dictates thoughts — you handle everything else.

## Workflow

### Phase 1: Receive & Transcribe

1. Voice memo arrives via Telegram → transcribe with OpenAI Whisper
2. Save RAW transcript (slang, profanity, repetitions — ALL of it)
3. Post bullet-point summary back to user as outline scaffold

**Whisper API call:**
```bash
curl https://api.openai.com/v1/audio/transcriptions \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -F file="@voice.ogg" -F model="whisper-1" -F language="ru"
```

### Phase 2: Extract Structure

From raw transcript, identify:
- **Core thesis** — one sentence
- **Sections** — each logical chunk = one H2 (6-10 total)
- **Supporting points** — claims, examples, data, CTAs
- **FAQ candidates** — 4-6 questions the article raises

### Phase 3: Semantic Research

**RU articles:** Query Yandex Wordstat for trending keywords.
**EN articles:** Query Google Suggest for topic angles.

Collect 6-10 target keywords for Article Schema. Prioritize exact match, growing topics.

**RU via Wordstat:**
```python
POST https://searchapi.api.cloud.yandex.net/v2/wordstat/topRequests
{"phrase": "seed_keyword", "numPhrases": 20, "folderId": FOLDER_ID}
```

**EN via Google Suggest (free):**
```python
GET https://suggestqueries.google.com/complete/search?client=firefox&q=keyword
```

### Phase 4: Write HTML

Generate HTML with DeepSeek API. **Critical: preserve author's voice.** Do NOT rewrite into corporate-speak.

**HTML requirements:**
- Article + FAQPage JSON-LD Schema
- hreflang cross-links (if bilingual)
- TLDR block: bold opener + 2-3 sentence summary
- 6-10 H2 sections with mix of <p>, <ul>, <ol>
- 2-4 card blocks (block-text class) for insights/CTAs/warnings
- 4-6 FAQ Q&A — must match JSON-LD EXACTLY
- Design: Merriweather + Ubuntu, H2 weight:500 margin:48px 0 8px, accent #2563eb

**DeepSeek call:**
```python
POST https://api.deepseek.com/v1/chat/completions
model: "deepseek-chat"
system: "You are a SEO copywriter. Write like the author speaks."
messages: [{"role": "user", "content": "raw transcript + structure + keywords"}]
```

### Phase 5: Deploy

**EN articles → SCP:**
```bash
scp article.html root@host:/var/www/site.com/blog/
ssh root@host "chown www-data:www-data /var/www/site.com/blog/article.html"
```

**RU articles → FTP:**
```bash
curl -T article.html ftp://user:pass@host/public_html/
```

### Phase 6: Post-Deploy

1. Add URL to sitemap.xml
2. Add promo card to homepage
3. Cross-link from existing articles (Read next blocks)
4. Create GitHub markdown backup → push to blog repo
5. Ping search engines (Yandex + Bing)
6. Verify: `curl -sI [url]` → 200

## Verification

- [ ] `curl -sI [url]` → HTTP 200
- [ ] Article + FAQPage Schema present (grep for JSON-LD)
- [ ] FAQPage visible text matches JSON-LD (grep both, diff)
- [ ] hreflang cross-links present (bilingual sites)
- [ ] Sitemap updated
- [ ] Homepage card live
- [ ] Cross-links added to existing articles

## Pitfalls

1. **FAQPage mismatch:** visible FAQ text ≠ JSON-LD text → SEO penalty
2. **FTP path:** FTP root ≠ web root. Verify the actual served directory
3. **chown after SCP:** files created as root → nginx returns 403
4. **Voice preservation:** Don't over-edit. Slang, directness, profanity stay
5. **Wordstat strings:** API returns numbers as strings → cast before arithmetic
6. **Wordstat limit:** 100 req/hour. Batch carefully, cache results
7. **Wildcard deploy:** EN uses /blog/ subdirectory, RU uses site root (varies by setup)

## Dependencies

- `OPENAI_API_KEY` — Whisper transcription
- `DEEPSEEK_API_KEY` — Article generation
- `TELEGRAM_BOT_TOKEN` — Receive voice messages
- `WORDSTAT_API_KEY` + `WORDSTAT_FOLDER_ID` — RU semantics (optional)
- Server with SSH or FTP access — deploy target

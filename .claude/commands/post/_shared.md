# Shared — loaded by all /post flows

Today's date: read from system (YYYY-MM-DD).

## Step 0 — Startup checks

### 0A. Read config/profile.md
Extract: NAME, ROLE, INDUSTRY, NICHE_TOPICS, AUDIENCE, TONE, FORMAT, VOICE, POST_LENGTH, EMOJI_USAGE, HASHTAG_COUNT, AVOID, GOALS, SAMPLE_1/2/3.
If NAME is empty → stop: "Run `/post sync` first to fill in config/profile.md, or edit it manually."

### 0B. Read config/slack.md
If WEBHOOK_URL is not "YOUR_WEBHOOK_URL" → slack_enabled=true. Else slack_enabled=false.

### 0C. Chrome check
Call `mcp__Claude_in_Chrome__tabs_context_mcp` (createIfEmpty:true). Fail → stop: "Chrome not connected."
Create a new tab. Navigate to `https://www.linkedin.com/in/me/`. Read page.
Redirected to login → stop: "Log in to LinkedIn in Chrome first."
Success → print: `✓ Chrome · LinkedIn: <name>`

## Output

**Save draft to:** `posts/draft_YYYY-MM-DD_<2-3-word-slug>.md`

File format:
```
# <Topic>
Date: YYYY-MM-DD | Topic: <topic> | Why: <one sentence>

---
<post text>
---
```

**Slack (if slack_enabled=true):**
```bash
curl -s -o /dev/null -w "%{http_code}" -X POST "WEBHOOK_URL" \
  -H "Content-Type: application/json" \
  -d "{\"text\": \"*LinkedIn Draft*\n\n<escaped post text>\n\n_File: posts/draft_<slug>.md_\"}"
```
Non-200 → warn user, draft already saved locally.

## Post writing rules
- No em-dashes (—). Scan before output.
- Mirror TONE, FORMAT, VOICE, POST_LENGTH, EMOJI_USAGE, HASHTAG_COUNT from profile.
- First line = scroll-stopping hook. Specific, direct, or surprising.
- No filler openers: "In today's world", "As a software engineer", "Hot take:", "I've been thinking about".
- No AI phrases: "delve", "it's worth noting", "the importance of".
- End with a genuine question or CTA.
- Hashtags on their own line at the end.

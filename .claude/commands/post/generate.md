# GENERATE

## Step 1 — Load context
Run Step 0 from _shared.md. Hold profile data in memory.
topic_hint = any text passed after `/post` (empty if none).

## Step 1B — Read performance history
Read `posts/tracker.csv` (silently, no output to user).
If the file has 1+ rows with Posted=yes, extract:
- **avoid_topics**: topics from the 3 lowest-engagement posts (fewest comments) — don't suggest these again
- **best_format**: format with the highest average comments across all posted rows
- **insight**: if 5+ rows exist, compute one sentence: e.g. "Story posts average 3x more comments than lists for you."

Hold these as performance_context. If tracker is empty or has no Posted=yes rows, performance_context = null.

## Step 2 — Style samples
If SAMPLE_1 in config/profile.md is filled → use those. Skip Chrome navigation.
If all samples are empty → navigate to `https://www.linkedin.com/in/me/recent-activity/shares/`, read page, extract last 3 post texts. Hold as style_samples.

## Step 3 — Research (1 web search + 1 Chrome search)

**3A. Web search — 1 query only:**
Query: `top linkedin posts "<INDUSTRY>" "<primary NICHE_TOPIC>" 2025 OR 2026`
Extract from results: hook/first line, post angle or format (story, list, tip, contrarian), engagement signals if shown. Take top 5 results.

**3B. Chrome LinkedIn search — 1 query only:**
Navigate to:
`https://www.linkedin.com/search/results/content/?keywords=<primary_niche_topic_url_encoded>&datePosted=past-month&sortBy=relevance`
Read page. Extract: hook, author role, comment count (prefer posts with comments), format. Take 4-5 posts.

**3C. Summarize research in 3 lines (internal, don't show user):**
- Top formats performing now
- Top topics getting traction
- Hook patterns that appear most

## Step 4 — Suggest 3 topics

Using research summary + profile niche/goals + topic_hint + performance_context, generate 3 ideas.
If topic_hint given → at least one idea expands it.
Skip topics already covered in style_samples.
If performance_context is set: skip any idea that overlaps with avoid_topics; prefer best_format for at least one idea.

If performance_context has an insight line → show it before the list:
```
Note: <insight line from performance_context>
```

Show:
```
3 topic ideas:

1. **<Title>** — <hook angle in one sentence> | Format: <format>
2. **<Title>** — <hook angle in one sentence> | Format: <format>
3. **<Title>** — <hook angle in one sentence> | Format: <format>

Pick 1, 2, or 3 — or say "more" for new ideas.
```

Wait. On "more" → repeat Step 3 with a different niche topic query, then re-generate.

## Step 4B — Pick tone variant

After the user picks a topic, ask:

```
Tone for this post:

1. **Default** — your usual style from profile
2. **Bold / Contrarian** — strong opinion, challenges common thinking
3. **Personal story** — first-person narrative, vulnerability, lesson at the end
4. **Educational** — clear breakdown, teach something, structured steps
5. **Motivational** — energy, aspiration, rallying the reader

Pick 1-5 (or press Enter for Default):
```

Wait. Store as `tone_variant`. If Enter/blank → tone_variant = "default".

## Step 5 — Write

Write the post using the chosen topic + style_samples + profile style fields + tone_variant.

Tone variant rules:
- **default**: mirror TONE/FORMAT/VOICE from profile exactly
- **bold/contrarian**: open with a provocative claim, back it with evidence or experience, no hedging language
- **personal story**: open with a scene or moment (not "I"), build to one clear lesson, close with a relatable question
- **educational**: hook → numbered steps or short sections → one-line takeaway → question
- **motivational**: punchy short sentences, second-person ("you"), close with a call to action

Rules (from _shared.md): no em-dashes, strong hook, match format/length/emoji/hashtags from profile.

Show:
```
Draft: [<tone_variant> tone]
---
<post text>
---
Words: <N> | Save to: posts/draft_<date>_<slug>.md

Good? Say "save", request changes, or "switch tone" to rewrite in a different variant.
```

Wait. Revise on request. On "switch tone" → jump back to Step 4B. On "save" → Step 6.

## Step 6 — Save + deliver

Write `posts/draft_YYYY-MM-DD_<slug>.md` using the output format from _shared.md.
If slack_enabled=true → run the curl command from _shared.md.
Print result: `✓ Saved: posts/draft_<slug>.md` (+ `✓ Slack` if sent).

# SYNC — Pull profile from LinkedIn into config/profile.md

Run once on setup. Re-run when your focus or style changes.

## Step 1
Run Step 0B and 0C from _shared.md (skip 0A profile check — that's what we're fixing).
Print: `Syncing from LinkedIn...`

## Step 2 — Read profile page
Navigate to `https://www.linkedin.com/in/me/`. Read page text.
Extract: full name, headline, about section (click "see more" if collapsed), current company/title, location.

## Step 3 — Read recent posts
Navigate to `https://www.linkedin.com/in/me/recent-activity/shares/`. Read page.
Extract last 5 posts: full text + reaction/comment counts if visible.

## Step 4 — Analyze style (internal, don't show user)
From the 5 posts, note: avg word count, tone, format patterns, hook types, emoji usage, hashtag count/style, recurring topics, highest-engagement post.

## Step 5 — Write config/profile.md
Read current config/profile.md. Fill in or update:
- NAME, ROLE (from headline), INDUSTRY (infer from about + posts), EXPERIENCE_YEARS (estimate)
- NICHE_TOPICS (from recurring post topics + about section)
- TONE, FORMAT, VOICE (from Step 4 analysis)
- SAMPLE_1, SAMPLE_2, SAMPLE_3 (3 best posts — highest engagement, or most recent)

**Preserve any fields the user already filled in. Only overwrite empty or placeholder fields.**

## Step 6 — Confirm
Print a short summary:
```
✓ Synced

Updated: NAME, ROLE, NICHE_TOPICS, style fields, 3 post samples
Kept: <any fields already filled>

Review config/profile.md if anything looks off.
Run /post to generate your first post.
```

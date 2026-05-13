# IDEA — Rapid post idea brainstorm

Use this to generate a bank of post ideas without writing any drafts.
Run `/post idea` or `/post idea <theme>` for focused brainstorm.

No Chrome needed unless samples are missing.

## Step 1 — Load context

Run Step 0A and 0B from _shared.md (skip Chrome check 0C — not needed here).
theme = any text passed after `/post idea` (empty if none).

Read `posts/tracker.csv` silently. Extract:
- avoid_topics: topics from 3 lowest-engagement posted rows (fewest comments)
- best_format: format with highest avg comments
If tracker empty or no Posted=yes rows → skip.

## Step 2 — Generate ideas

Generate 8 post ideas using: profile NICHE_TOPICS + GOALS + AUDIENCE + theme (if given) + tracker data.

Rules:
- Skip avoid_topics
- Include at least one idea using best_format (if known)
- Cover at least 3 different formats across the 8 ideas
- Each idea must be distinct — no overlapping angles
- Skip topics covered in SAMPLE_1/2/3

Formats to pull from: personal story, numbered list, contrarian take, hot tip, lessons learned, case study, question-led, behind-the-scenes.

Show:
```
8 post ideas:

1. **<Title>** — <hook angle, 1 sentence> | Format: <format> | Tone: <tone>
2. ...
...
8. ...

Say a number to write that post now, "save ideas" to store the list, or "more" for a fresh batch.
```

Wait for response:
- Number → load generate.md Step 4B with that topic pre-selected (skip topic suggestion), then write
- "save ideas" → Step 3
- "more" → re-run Step 2 with a different angle on the niche topics
- "more <theme>" → re-run Step 2 with that theme

## Step 3 — Save idea bank (optional)

Write `posts/ideas_YYYY-MM-DD.md`:

```
# Post Ideas — YYYY-MM-DD

<numbered list of all ideas shown, one per line with format and tone>
```

Print: `✓ Saved: posts/ideas_YYYY-MM-DD.md`

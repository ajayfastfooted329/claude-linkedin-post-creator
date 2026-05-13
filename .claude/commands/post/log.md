# LOG — Record engagement for a published post

Use this after you post to LinkedIn. Run `/post log` to pick a draft, mark it posted, and record likes/comments/shares.

No Chrome needed.

## Step 1 — Show unlogged drafts

Read `posts/tracker.csv`. Read all `draft_*.md` files in `posts/`.
Find drafts that are NOT yet in tracker.csv (match by slug from filename).

If all drafts are already logged:
> All drafts are logged. Nothing new to record.
Show the tracker table and exit.

Show unlogged drafts as a numbered list:
```
Unlogged drafts:
1. draft_2026-05-13_react-server-components.md — React Server Components
2. draft_2026-05-14_career-growth-tips.md — Career Growth Tips
...

Which one did you post? (enter number, or "all" to log multiple)
```

Wait for response.

## Step 2 — Collect engagement

For each selected draft, ask:
```
<Topic> — enter engagement (or press Enter to skip a field):
Likes: 
Comments: 
Shares: 
Notes (optional — e.g. "got lots of DMs", "flopped", "wrong audience"):
```

Wait for input. Accept blank for any field (store as 0).

## Step 3 — Append to tracker.csv

For each logged post, append a row to `posts/tracker.csv`:
```
Date,Slug,Topic,Format,Likes,Comments,Shares,Posted,Notes
```

- **Date** — from the draft filename (YYYY-MM-DD)
- **Slug** — from the draft filename (e.g. `react-server-components`)
- **Topic** — from the draft file's Topic field
- **Format** — from the draft file's format (e.g. "numbered list", "personal story", "contrarian take") — read from the draft file Style notes line
- **Likes/Comments/Shares** — from user input (0 if blank)
- **Posted** — yes
- **Notes** — from user input (empty if blank)

Preserve all existing rows exactly. Only append new rows.

## Step 4 — Show insight (if 5+ posted entries exist)

Read all rows in tracker.csv where Posted=yes.
If 5 or more rows exist, compute and show a brief performance insight:

```
Performance snapshot (last <N> posts):

Best format: <format with highest avg comments>
Avg likes: <number>
Avg comments: <number>
Top post: "<topic>" — <likes> likes, <comments> comments

<one sentence insight, e.g. "Story-format posts get 3x more comments than list posts for you.">
```

If fewer than 5 entries → skip the insight silently.

## Step 5 — Confirm
```
✓ Logged <N> post(s) to posts/tracker.csv
```

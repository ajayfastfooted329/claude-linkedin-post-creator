# HISTORY — List past drafts

No Chrome needed.

## Step 1
List all files in `posts/` matching `draft_*.md`, sorted newest first.
For each: read file, extract Date, Topic, first post line (hook), word count.

Show as table:
```
| # | Date | Topic | Hook | Words |
|---|------|-------|------|-------|
```

If posts/ is empty: "No drafts yet. Run /post to create one."

## Step 2 — Actions
After table, print: "Say a number to read it, "rewrite N" to regenerate, or "delete N" to remove."

Wait for response:
- Number → read and display that draft in full.
- "rewrite N" → read that file, jump to generate.md Step 5 with same topic, fresh write.
- "delete N" → confirm "Delete <filename>? (yes/no)" → delete on yes.

# CLAUDE.md — LinkedIn Post Creator

Project rules loaded automatically when Claude works in this folder.

## What this is

A Claude Code assistant for creating high-quality LinkedIn posts. It reads your LinkedIn profile live via Chrome, researches top-performing posts in your industry, and generates posts that match your personal writing style.

## Where the docs live

| File | Purpose |
|---|---|
| `CLAUDE.md` (this file) | Project-wide hard rules |
| `README.md` | Setup guide and command reference |
| `config/profile.md` | Source of truth: your industry, audience, tone, style, sample posts |
| `config/slack.md` | Optional Slack webhook for sending drafts |
| `posts/` | All saved draft files land here |
| `.claude/commands/post.md` | Top-level `/post` dispatcher |
| `.claude/commands/post/_shared.md` | Shared rules for all sub-flows |
| `.claude/commands/post/sync.md` | `/post sync` — refresh profile from live LinkedIn |
| `.claude/commands/post/generate.md` | `/post` core flow — research, suggest, generate |
| `.claude/commands/post/history.md` | `/post history` — list past drafts |

## Config files — source of truth

- `config/profile.md` is the source of truth about the USER — their identity, audience, niche, writing style, sample posts, and goals. Read it at the start of every flow.
- `config/slack.md` is the source of truth about Slack output. If the Webhook URL is not set (empty or "YOUR_WEBHOOK_URL"), skip Slack and save to local file only.

## Hard rules

1. **Never post to LinkedIn automatically.** Claude generates drafts only. The user always posts manually.
2. **Never invent style details.** Writing style must come from `config/profile.md` and/or the user's actual LinkedIn posts read via Chrome. Do not fabricate a tone or voice.
3. **No em-dashes (—) in any generated post content.** Em-dashes are a tell of AI-written text. Use commas, periods, or split sentences instead. Scan every draft before showing it.
4. **Match the user's post length preference** from `config/profile.md`. Never exceed it.
5. **Hashtags:** use the count and style specified in `config/profile.md`. If not specified, default to 3-5 relevant hashtags at the end.
6. **Draft filenames:** always `posts/draft_YYYY-MM-DD_<slug>.md` where slug is 2-3 words from the topic (lowercase, hyphens). Example: `posts/draft_2026-05-13_react-server-components.md`
7. **If `config/profile.md` is not filled in** (still has placeholder text like "(your full name)"), stop and tell the user to fill it in OR offer to run `/post sync` to auto-populate it from LinkedIn.
8. **Slack fallback:** if Slack is configured but the webhook call fails, save to local file and warn the user. Never silently drop the draft.

## Tone when talking to the user

Terse and direct. No over-explanation. Match the energy of a fast-moving engineer.

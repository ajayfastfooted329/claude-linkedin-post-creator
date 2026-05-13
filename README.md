<p align="center">
  <img src="https://img.shields.io/badge/Claude%20Code-Required-orange?style=for-the-badge" alt="Claude Code">
  <img src="https://img.shields.io/badge/LinkedIn-Chrome%20MCP-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn">
  <img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge" alt="License">
</p>

<h1 align="center">Claude LinkedIn Post Creator</h1>

<p align="center">
  <strong>Research. Generate. Track. Improve.</strong><br>
  A Claude Code assistant that reads your live LinkedIn profile, researches what's actually performing in your industry right now, and generates posts in your exact writing style.
</p>

<p align="center">
  <a href="#-how-it-works">How it works</a> ·
  <a href="#-quick-start">Quick Start</a> ·
  <a href="#-commands">Commands</a> ·
  <a href="#-tone-variants">Tone Variants</a> ·
  <a href="#-performance-tracking">Performance Tracking</a> ·
  <a href="#-slack-setup">Slack Setup</a> ·
  <a href="#-configuration">Configuration</a>
</p>

---

## What makes this different

Most LinkedIn tools give you generic posts. This one reads **your** profile, researches **your** industry live, and writes in **your** voice — then learns from which of your posts actually perform.

| Feature | What it does |
|---|---|
| Live profile read | Reads your LinkedIn about, headline, and recent posts via Chrome — no copy-pasting |
| Industry research | 1 web search + 1 LinkedIn search before every post — grounded in what's working right now |
| Style matching | Mirrors your actual tone, format, length, emoji usage, and hook patterns |
| 5 tone variants | Same topic, different energy: Default, Bold/Contrarian, Personal Story, Educational, Motivational |
| Idea bank | Generate 8 post ideas at once — save them for later or pick one to write immediately |
| Performance tracking | Log likes/comments/shares — Claude avoids your low-performers and leans into your best format |
| Slack delivery | Optional: sends every draft to a Slack channel for team review |
| No code, no API keys | Pure markdown slash commands — nothing to install or configure beyond Claude Code |

**You always post manually.** This tool generates drafts only — never touches your LinkedIn account.

---

## How it works

There is no code to install and no npm packages. The entire assistant is markdown files in `.claude/commands/` — Claude Code reads them as instructions.

LinkedIn is accessed via the **Claude in Chrome extension**, which lets Claude navigate URLs and read page content in your open browser. It drives Chrome like a person would: reads your profile, searches LinkedIn for top posts in your niche, extracts hooks and engagement signals.

```
You type /post
       ↓
Claude reads your config/profile.md
       ↓
Checks posts/tracker.csv → learns from your past performance
       ↓
1 web search + 1 LinkedIn search → finds top posts in your industry today
       ↓
Suggests 3 topic ideas (filtered by what worked for you before)
       ↓
You pick a topic → pick a tone variant
       ↓
Claude writes a post in your exact style
       ↓
You approve → saved to posts/ and optionally sent to Slack
```

---

## Prerequisites

You need two things before anything else:

**1. Claude Code desktop app**
Download from [claude.ai/download](https://claude.ai/download). Must be the desktop app — the web version cannot access local files or drive Chrome extensions.

**2. Claude in Chrome extension**
Install from [claude.com/claude-in-chrome](https://claude.com/claude-in-chrome). This is how Claude reads your LinkedIn. After installing:
- Sign in to LinkedIn in that Chrome window
- Keep Chrome open whenever you run a `/post` command

---

## Quick Start

### 1. Clone the repo

```bash
git clone https://github.com/tarunkorat/claude-linkedin-post-creator.git
cd claude-linkedin-post-creator
```

### 2. Open in Claude Code

Launch the **Claude Code desktop app** → **File → Open Folder** → select the `claude-linkedin-post-creator` folder.

### 3. Sync your profile from LinkedIn

In the Claude Code chat, run:

```
/post sync
```

Claude will navigate to your LinkedIn profile via Chrome, extract your about section, headline, recent posts, and writing style — and fill in `config/profile.md` automatically. This is the recommended first step.

**Or** open `config/profile.md` manually and fill in the fields yourself.

### 4. Generate your first post

```
/post
```

Claude suggests 3 topic ideas. Pick one, choose a tone, and Claude writes the full post.

---

## Commands

| Command | What it does |
|---|---|
| `/post` | Suggest 3 research-backed topic ideas, pick one, generate a post |
| `/post <topic>` | Same flow but with your topic as a starting hint |
| `/post idea` | Brainstorm 8 post ideas fast — save to a file or pick one to write |
| `/post idea <theme>` | Brainstorm 8 ideas focused on a specific theme |
| `/post sync` | Read your live LinkedIn profile and update `config/profile.md` |
| `/post history` | View, read, rewrite, or delete past drafts |
| `/post log` | Record likes/comments/shares for a published post |

---

## The Generate Flow — step by step

When you run `/post`, here is exactly what happens:

**Step 1 — Load your profile**
Reads `config/profile.md` for your industry, niche topics, tone, and style. If it's not filled in, Claude stops and tells you to run `/post sync`.

**Step 2 — Check your performance history**
Reads `posts/tracker.csv` silently. If you have past posts logged:
- Avoids topics from your 3 lowest-engagement posts
- Favors the format that gets you the most comments
- Shows you a one-line performance insight if you have 5+ posts logged

**Step 3 — Get your writing style**
If you have samples in `config/profile.md`, uses those (fast, no Chrome). Otherwise navigates to your LinkedIn activity to extract your last 3 posts.

**Step 4 — Research your industry**
1 web search for top LinkedIn posts in your industry + 1 LinkedIn search for recent high-comment posts in your niche. Claude extracts hooks, formats, and angles from 8-10 real posts before suggesting anything.

**Step 5 — Suggest 3 topic ideas**
Each idea shows a title, hook angle, and format. If your performance history has an insight, it appears here.

**Step 6 — Pick a tone variant**
After choosing a topic, you pick how it sounds. See [Tone Variants](#-tone-variants) below.

**Step 7 — Write and review**
Claude writes the full post. You see the draft with word count. Say `save`, request changes, or `switch tone` to rewrite in a different variant.

**Step 8 — Save and deliver**
Draft saved to `posts/draft_YYYY-MM-DD_<slug>.md`. If Slack is configured, sent to your channel automatically.

---

## Tone Variants

After picking a topic, Claude asks which tone to write in:

| # | Tone | Best for |
|---|---|---|
| 1 | **Default** | Your normal style from `config/profile.md` |
| 2 | **Bold / Contrarian** | Strong opinions, challenging common thinking — high engagement |
| 3 | **Personal Story** | First-person narrative with a lesson at the end — builds trust |
| 4 | **Educational** | Clear breakdown, numbered steps, structured teach — authority |
| 5 | **Motivational** | Short punchy sentences, second-person, call to action — energy |

You can say **"switch tone"** after seeing a draft to rewrite the same post in a different variant — no need to start over.

---

## Post Idea Bank

```
/post idea
/post idea career growth
```

Generates **8 post ideas at once** — no drafts, just rapid brainstorm. Useful when you want to plan a week of content or explore angles before committing.

- Covers at least 3 different formats per batch (story, list, contrarian, tip, etc.)
- Respects your tracker data — skips your low-performers, includes at least one idea in your best format
- Say a number to immediately write that post, `save ideas` to store the full list to `posts/ideas_YYYY-MM-DD.md`, or `more` for a fresh batch

---

## Performance Tracking

The more you use this tool, the smarter it gets.

### Log a post after publishing

After you post to LinkedIn, run:

```
/post log
```

Claude shows your unlogged drafts. Pick one and enter your engagement:

```
Career Growth Tips — enter engagement (or press Enter to skip):
Likes: 47
Comments: 12
Shares: 3
Notes: got 3 DMs from this one
```

### What Claude learns

Data is stored in `posts/tracker.csv`. On every future `/post` run:

- **Avoids** topics from your 3 lowest-engagement posts
- **Favors** the format with the highest average comments for you
- **Shows** a performance insight once you have 5+ posts logged, e.g.:
  > "Story-format posts get 3x more comments than list posts for you."

The more you log, the more accurate the suggestions become.

### View your performance snapshot

After logging, if you have 5+ posts recorded, Claude shows:

```
Performance snapshot (last N posts):

Best format: personal story
Avg likes: 34
Avg comments: 8
Top post: "Why I quit my senior role" — 89 likes, 24 comments

Story posts average 3x more comments than list posts for you.
```

---

## Slack Setup

Slack is optional. If not configured, drafts are saved to `posts/` only.

### 1. Create a Slack webhook

1. Go to [api.slack.com/apps](https://api.slack.com/apps) → **Create New App → From scratch**
2. Name it (e.g. "LinkedIn Drafts"), pick your workspace
3. Go to **Incoming Webhooks** → toggle **Activate Incoming Webhooks** ON
4. Click **Add New Webhook to Workspace** → pick a channel (e.g. `#linkedin-drafts`) → **Allow**
5. Copy the webhook URL — it starts with `https://hooks.slack.com/services/...`

### 2. Add it to config

Open `config/slack.md` and paste your webhook URL:

```
WEBHOOK_URL: https://hooks.slack.com/services/YOUR/WEBHOOK/URL
CHANNEL: #linkedin-drafts
ENABLED: true
```

After this, every approved draft is automatically sent to your Slack channel. If the webhook fails, Claude saves locally and warns you — no drafts are ever silently dropped.

---

## Configuration

### `config/profile.md`

The source of truth about you. All post generation reads from here.

| Field | What to fill in | Example |
|---|---|---|
| `NAME` | Your full name | `Tarun Korat` |
| `ROLE` | Your current title | `Senior Software Engineer` |
| `INDUSTRY` | Your industry | `Software Engineering` |
| `EXPERIENCE_YEARS` | Years in your field | `7` |
| `AUDIENCE` | Who reads your posts | `Junior-to-mid engineers, tech leads, startup founders` |
| `NICHE_TOPICS` | Your focus areas (comma-separated) | `JavaScript, system design, AI tools, career growth` |
| `TONE` | How you sound | `Conversational, direct, no fluff` |
| `FORMAT` | Your post structure | `Short sentences, lots of line breaks, occasional bullet lists` |
| `VOICE` | POV and style | `First person, shares personal opinions and stories` |
| `POST_LENGTH` | Target word count | `150-300 words` |
| `EMOJI_USAGE` | How many and where | `Minimal, 1-2 per post, never mid-sentence` |
| `HASHTAG_COUNT` | Number of hashtags | `3-5` |
| `AVOID` | Topics to never write about | `Politics, hustle culture, generic motivational quotes` |
| `GOALS` | Why you post on LinkedIn | `Build personal brand, attract senior engineering roles` |
| `SAMPLE_1/2/3` | Your best posts (paste text) | *(or run `/post sync` to auto-fill)* |

**Using a different industry?** Just change `INDUSTRY` and `NICHE_TOPICS`. The entire system adapts — research queries, topic suggestions, and style matching all use these fields.

### `config/slack.md`

Three fields: `WEBHOOK_URL`, `CHANNEL`, `ENABLED`. See [Slack Setup](#-slack-setup).

---

## Folder layout

```
claude-linkedin-post-creator/
│
├── CLAUDE.md                          ← project rules (loaded automatically by Claude)
├── README.md                          ← this file
│
├── config/
│   ├── profile.md                     ← YOUR profile, style, industry, goals
│   └── slack.md                       ← Slack webhook config (optional)
│
├── posts/                             ← all your drafts and idea banks land here
│   ├── draft_YYYY-MM-DD_<slug>.md     ← individual post drafts (gitignored)
│   ├── ideas_YYYY-MM-DD.md            ← saved idea bank files (gitignored)
│   └── tracker.csv                    ← performance data (NOT gitignored)
│
└── .claude/
    └── commands/
        ├── post.md                    ← /post dispatcher (routes all commands)
        └── post/
            ├── _shared.md             ← shared rules loaded by every flow
            ├── generate.md            ← /post core flow
            ├── idea.md                ← /post idea brainstorm flow
            ├── sync.md                ← /post sync
            ├── history.md             ← /post history
            └── log.md                 ← /post log
```

---

## Writing rules Claude always follows

These are enforced on every generated post — you never need to ask:

- **No em-dashes** (—) — a common AI tell, banned entirely
- **No filler openers** — "In today's world", "As a software engineer", "Hot take:", "I've been thinking about"
- **No AI phrases** — "delve", "it's worth noting", "the importance of"
- **Strong first line** — scroll-stopping hook, specific and direct
- **Ends with a question or CTA** — not a trailing hashtag or nothing
- **Hashtags on their own line** at the end

---

## Privacy

- `posts/draft_*.md` and `posts/ideas_*.md` are gitignored by default — your drafts stay local
- `posts/tracker.csv` is NOT gitignored (it's your performance data — you want to keep it)
- `config/profile.md` is NOT gitignored — if you store personal details you don't want public, use a private repo
- Claude never posts to LinkedIn automatically — all publishing is manual

---

## License

MIT

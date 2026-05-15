# VJ Personal Claude Package

Vinamra Jain's personal bundle of Claude skills. The single source of truth is this GitHub repo. Install it once in each Claude surface (Claude Code CLI, Claude Code inside the desktop app, and Cowork) to get a consistent skill set everywhere.

## What's inside

### Skills (auto-trigger when you describe a relevant task)

| Skill | What it does | Typical trigger phrases |
|---|---|---|
| **fundamental-analysis** | Produces an investment-grade fundamental analysis of a publicly listed equity — executive summary upfront, detailed report below, with verdict, fair value range, moats, financials, management, risks. | "should I invest in [ticker]", "fundamental analysis of [company]", "deep dive on [stock]", "is [ticker] fairly valued" |
| **pr-description** | Drafts a clear, well-structured pull request description from the actual changes on the current branch. | "write a PR description", "draft a PR", "summarize this branch for a PR" |
| **resume-tailor** | Tailors a resume to a specific job listing — analyses JD, researches the company, suggests targeted edits to maximise interview chances. | "tailor my resume", "optimize resume for job", "help me apply to [company]" |
| **supabase** | General-purpose Supabase development helper across Database, Auth, Edge Functions, Realtime, Storage, Vectors, Cron, Queues, and client libraries. | Any task involving Supabase products, `supabase-js`, `@supabase/ssr`, RLS, migrations, CLI, MCP |
| **supabase-postgres-best-practices** | Postgres performance and best-practices guide from Supabase — query optimisation, schema design, connection management, locking, indexing, security. | Writing, reviewing, or optimising Postgres queries or schemas |

### Slash commands (user-invoked)

| Command | What it does |
|---|---|
| `/save-progress` | Updates `CLAUDE.md`, `TODO.md`, `PROGRESS.md`, and `DECISIONS.md` with current session work so the next session can pick up seamlessly. Designed for end-of-session handoff. |

## How distribution works

- **Source of truth**: this GitHub repo. All edits happen here.
- **Claude Code** (CLI + in-app) pulls directly from GitHub via a single-plugin marketplace. Its local copy lives in `~/.claude/plugins/cache/` and is managed automatically — never edit it by hand.
- **Cowork** (desktop app) installs from a `.plugin` zip. A GitHub Action builds and attaches that zip to every release. To update Cowork you download the latest `.plugin` from the Releases page and drag it into the app.

## Installation

### Claude Code (CLI in terminal, and Claude Code inside the desktop app)

In any session:

```
/plugin marketplace add vinamrajain99/vj-personal-claude-package
/plugin install vj-personal-claude-package@vj-personal-claude-package
```

That's it. Future updates flow in via `/plugin marketplace update`.

### Cowork (Claude desktop app)

1. Go to `https://github.com/vinamrajain99/vj-personal-claude-package/releases`.
2. Download `vj-personal-claude-package.plugin` from the latest release.
3. Drag it onto the Claude desktop app window (or use Customize → install plugin).

## Repo layout (for reference)

```
vj-personal-claude-package/
├── .claude-plugin/
│   ├── marketplace.json     # makes this repo installable via /plugin marketplace add
│   └── plugin.json          # plugin manifest (name, version, author)
├── .github/
│   └── workflows/
│       └── build-plugin.yml # auto-builds .plugin on push & tags
├── .gitignore
├── README.md
├── commands/
│   └── save-progress.md     # slash command (legacy single-file format)
└── skills/
    ├── fundamental-analysis/
    │   └── SKILL.md
    ├── pr-description/
    │   └── SKILL.md
    ├── resume-tailor/
    │   └── SKILL.md
    ├── supabase/
    │   ├── SKILL.md
    │   ├── references/
    │   └── assets/
    └── supabase-postgres-best-practices/
        ├── SKILL.md
        └── references/
```

## Sources & credits

- `supabase` and `supabase-postgres-best-practices` skills originate from Supabase (MIT-licensed, bundled here for personal use).
- All other skills are personal.

## How I keep this updated

This workflow assumes nothing is set up locally. Start anywhere.

### 1. Get a working copy of the repo

**If you've never cloned it on this machine:**

```bash
git clone https://github.com/vinamrajain99/vj-personal-claude-package.git \
  ~/code/vj-personal-claude-package
cd ~/code/vj-personal-claude-package
```

`~/code/` is just a suggestion. Pick any directory you like for your working copy — but do **not** put it inside `~/.claude/` (that's where the installed copy lives, and the two would conflict).

**If you already have a clone:**

```bash
cd ~/code/vj-personal-claude-package && git pull
```

### 2. Edit the skill

Open `skills/<skill-name>/SKILL.md` and make your changes. References under `skills/<skill-name>/references/` are fair game too.

### 3. Bump the version

Edit both manifest files and increment the version (e.g., `0.1.0` → `0.1.1`):

- `.claude-plugin/plugin.json` — bump `version`
- `.claude-plugin/marketplace.json` — bump `metadata.version` **and** the `version` of the entry inside the `plugins` array

### 4. Commit, push, tag

```bash
git add .
git commit -m "Improve <skill-name>: <what changed>"
git push

# Cut a release so the GitHub Action builds a fresh .plugin
git tag v0.1.1
git push --tags
```

The Action takes ~30 seconds to build the `.plugin` and attach it to the Release.

### 5. Propagate to your installs

**Claude Code** (CLI + in-app), in any session:

```
/plugin marketplace update vj-personal-claude-package
```

**Cowork** (desktop app):

1. Open `https://github.com/vinamrajain99/vj-personal-claude-package/releases` and download the newly-tagged `vj-personal-claude-package.plugin`.
2. Drag it onto the Claude desktop app to overwrite the previous install.

### 6. (Optional) Tidy up

Your working clone at `~/code/vj-personal-claude-package` can stay for next time, or be deleted — the repo is the source of truth either way. Re-clone whenever you need it.

## How I add new skills

Same flow as updating, with one extra step at the start.

### 1. Get a working copy (see Step 1 of "How I keep this updated" above)

### 2. Create the new skill folder

```bash
cd ~/code/vj-personal-claude-package
mkdir -p skills/<new-skill-name>
```

Inside `skills/<new-skill-name>/SKILL.md`, start with valid YAML frontmatter:

```yaml
---
name: <new-skill-name>
description: One-paragraph description with specific trigger phrases. Be opinionated about when this skill should fire; the description is the primary mechanism for auto-triggering.
---

# <Human-readable title>

Instructions to Claude on how to perform the task. Imperative voice; explain the why where it helps.
```

Add `references/` and `assets/` subfolders if the skill needs supporting files.

### 3. Update this README

Add a row to the "What's inside" table at the top so future-you remembers what this skill does and how to trigger it.

### 4. Bump the version, commit, push, tag, propagate

Follow Steps 3–5 of the "How I keep this updated" flow.

# VJ Personal Claude Package

Vinamra Jain's personal bundle of Claude skills. Install this plugin once in each Claude surface (Claude Code CLI, Claude Code in the desktop app, and Cowork) to get a consistent skill set everywhere.

## What's inside

| Skill | What it does | Typical trigger phrases |
|---|---|---|
| **fundamental-analysis** | Produces an investment-grade fundamental analysis of a publicly listed equity — executive summary upfront, detailed report below, with verdict, fair value range, moats, financials, management, risks. | "should I invest in [ticker]", "fundamental analysis of [company]", "deep dive on [stock]", "is [ticker] fairly valued" |
| **pr-description** | Drafts a clear, well-structured pull request description from the actual changes on the current branch. | "write a PR description", "draft a PR", "summarize this branch for a PR" |
| **resume-tailor** | Tailors a resume to a specific job listing — analyses JD, researches the company, suggests targeted edits to maximise interview chances. | "tailor my resume", "optimize resume for job", "help me apply to [company]" |
| **supabase** | General-purpose Supabase development helper across Database, Auth, Edge Functions, Realtime, Storage, Vectors, Cron, Queues, and client libraries. | Any task involving Supabase products, `supabase-js`, `@supabase/ssr`, RLS, migrations, CLI, MCP |
| **supabase-postgres-best-practices** | Postgres performance and best-practices guide from Supabase — query optimisation, schema design, connection management, locking, indexing, security. | Writing, reviewing, or optimising Postgres queries or schemas |

## Installation

### Claude Code (CLI in terminal)

```bash
# From wherever the .plugin file is on disk:
/plugin install /path/to/vj-personal-claude-package.plugin
```

Or unzip directly into the user-level skills folder:

```bash
mkdir -p ~/.claude/skills
unzip vj-personal-claude-package.plugin -d /tmp/vj-plugin
cp -R /tmp/vj-plugin/skills/* ~/.claude/skills/
```

### Cowork (Claude desktop app)

Drag the `.plugin` file into the desktop app, or use the Customize → install plugin button.

### Claude Code inside the desktop app

Same as the CLI install above — it reads from the same `~/.claude/skills/` and `~/.claude/plugins/` locations.

## Layout

```
vj-personal-claude-package/
├── .claude-plugin/
│   └── plugin.json
├── skills/
│   ├── fundamental-analysis/
│   │   └── SKILL.md
│   ├── pr-description/
│   │   └── SKILL.md
│   ├── resume-tailor/
│   │   └── SKILL.md
│   ├── supabase/
│   │   ├── SKILL.md
│   │   ├── references/
│   │   └── assets/
│   └── supabase-postgres-best-practices/
│       ├── SKILL.md
│       └── references/
└── README.md
```

## Updating a skill

1. Edit the relevant `SKILL.md` (or files under `references/`) in the plugin source folder.
2. Bump the `version` field in `.claude-plugin/plugin.json` (e.g., `0.1.0` → `0.1.1`).
3. Re-package:
   ```bash
   cd "$HOME/Desktop/Claude-Work/Skills temp folder"
   rm -f vj-personal-claude-package.plugin
   (cd vj-personal-claude-package && zip -r /tmp/vj-personal-claude-package.plugin . -x "*.DS_Store")
   mv /tmp/vj-personal-claude-package.plugin .
   ```
4. Re-install the updated `.plugin` file in each surface.

## Adding a new skill

1. Create `skills/<new-skill-name>/SKILL.md` inside the plugin folder. The `SKILL.md` must start with YAML frontmatter containing at least `name` and `description`.
2. Add the skill to the table in this README.
3. Bump the version, repackage, reinstall (see above).

## Sources & credits

- `supabase` and `supabase-postgres-best-practices` skills originate from Supabase (MIT-licensed, bundled here for personal use).
- All other skills are personal.

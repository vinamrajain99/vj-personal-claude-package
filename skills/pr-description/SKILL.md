---
name: pr-description
description: >
  Generate a clear, well-structured pull request description for the current branch. Use this skill when the user asks to "write a PR description", "draft a PR", "summarize this branch for a PR", or is about to open a pull request and wants help writing the body. Trigger after work has been committed and the user is preparing to push or open a PR on GitHub.
---

# PR Description Skill

You help the user produce a high-quality pull request description based on the actual changes on the current branch.

---

## Workflow

### Step 1 — Gather context

Run these in parallel via Bash:
- `git status` — check working tree state
- `git log <base>..HEAD --oneline` — list commits on this branch (default base: `main` or `master`)
- `git diff <base>...HEAD` — full diff of changes vs. the base branch
- `gh pr view --json title,body 2>/dev/null` — if a PR already exists, read its current body so you can update rather than overwrite intent

If the base branch is unclear, ask the user before guessing.

### Step 2 — Analyze the changes

Look across **all** commits on the branch, not just the latest. Identify:
- The user-visible change (what behavior is different)
- The motivation (why — bug fix, feature, refactor, perf, etc.)
- Risk areas (migrations, breaking changes, config, infra)
- What tests or manual checks were added

### Step 3 — Draft the description

Default structure (adapt to repo conventions if a `.github/PULL_REQUEST_TEMPLATE.md` exists — read it first and follow it):

```
## Summary
- 1–3 bullets, focused on the *why* and the user-visible *what*

## Changes
- Concrete list of what was modified, grouped logically

## Test plan
- [ ] Checklist of how this was / should be verified

## Notes
- Anything reviewers should know: rollout order, follow-ups, known limitations
```

### Step 4 — Output

Print the drafted description to the user. Do **not** run `gh pr create` or `gh pr edit` unless they explicitly ask you to.

---

## Quality bar

- Title under 70 characters, imperative mood ("Add X", not "Added X" or "This adds X")
- Lead with the *why*, not a file-by-file recap — reviewers can read the diff
- No filler ("This PR makes some changes to..."). Be direct.
- Flag anything risky explicitly (schema changes, feature flags, breaking API changes)
- If the branch is multi-commit and the commits already tell a clean story, reference them rather than re-listing every change

# factory-template

A GitHub Template repo for spinning up new tools in the Personal Software Factory.

This repo's **"Template repository"** toggle is ON, so each new tool starts fresh by clicking **"Use this template"** in the GitHub UI — no shared git history, no shared issues, independent CI.

---

## What's in here

The minimum boilerplate every factory tool starts with:

- **`AGENTS.md`** — per-tool rules for Claude Code, with placeholders to fill in
- **`docs/PRD.md`** — empty PRD structure (problem, intent, scope, success/kill criteria, data model)
- **`docs/JOURNAL.md`** — append-only journal with the expected entry format
- **`docs/adr/0000-template.md`** — ADR template
- **`.github/workflows/ci.yml`** — Ruff lint + format check + pytest, runs on every PR
- **`.github/PULL_REQUEST_TEMPLATE.md`** — PR template referencing AGENTS.md
- **`pyproject.toml`** — Python 3.13, Ruff config, pytest config (replace `name` after stamping)
- **`requirements.txt`** / **`requirements-dev.txt`** — empty runtime + Ruff/pytest dev set
- **`.gitignore`** — Python, venv, IDE, .env, scratch dirs
- **`.env.example`** — placeholder for per-tool env vars (Supabase, OpenAI, etc.)
- **`learnings/README.md`** — placeholder explaining what goes here
- **`tests/`** — empty package skeleton

The factory's **default stack is Next.js + Drizzle + Supabase** (see `factory-meta/stack.md`). This template currently scaffolds **Python** because:

1. The first tool extracted from (`stock-recommender-v2`) is Python, so that's what we have.
2. The factory's principle of "per-tool stack flexibility" means tools may diverge with PRD justification.

**For a Next.js tool**, after stamping the template: delete `pyproject.toml`, `requirements*.txt`, the Python CI workflow, and follow the default stack per `factory-meta/stack.md`.

---

## How to use this template

1. **Pick a slug.** Short, lowercase, kebab-case. e.g. `meeting-notetaker`, `inbox-zero`, `weekly-meal-planner`.
2. **Click "Use this template" → "Create a new repository"** on this repo's page.
3. Name the new repo `pratkuk/<slug>`. Description = one sentence on what it does.
4. **Clone, then:**
   - Edit `pyproject.toml` → replace `name = "TODO-tool-slug"` with your slug
   - Edit `AGENTS.md` → fill in the `<<TOOL-SPECIFIC>>` placeholders (what the tool does, its rules)
   - Write `docs/PRD.md` — at minimum: Problem, Intent, Scope, Success criteria, Kill criteria, Data model
   - First commit: "v0.1 foundation"
5. **Add a row to `factory-meta/registry.md`** with the tool's name, repo URL, and a one-line description.
6. **Wire any secrets** the tool needs as GitHub repo secrets (Settings → Secrets and variables → Actions).
7. **Push, open PR #1 against your own main, merge.**

After that, follow the per-tool conventions in `AGENTS.md` for ongoing work.

---

## What this template intentionally doesn't include

- **CLAUDE.md** — Claude Code reads `AGENTS.md` by default; we don't maintain two files.
- **License** — Add per-tool if/when the tool gets distributed; most factory tools are personal.
- **CHANGELOG.md** — `docs/JOURNAL.md` is the source of truth for what shipped.
- **Issue templates** — Solo tools don't need them. Add later if collaborators join.
- **Dependabot** — Add per-tool if you want it.

---

## How this template stays current

When a meaningful pattern emerges in any factory tool that should propagate to the template, open a PR here. **The template doesn't auto-update existing tools** — that's intentional. Each tool drifts on its own clock; the boring-tool rule applies to the factory itself.

See `factory-meta/AGENTS.md` §"How to use the templates" for the canonical extraction protocol.

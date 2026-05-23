# AGENTS.md — Per-Tool Instructions

> Claude Code reads this at the start of every session inside this repo. It defines how to work here. Replace every `<<TOOL-SPECIFIC>>` placeholder before the first real commit.

## What this repo is

<<TOOL-SPECIFIC: one paragraph on what this tool does, who uses it, and how it fits into the Personal Software Factory. See `docs/PRD.md` for full intent and scope.>>

## Canonical source

The principles restated below are **summaries** for convenience. The canonical versions live in the `factory-meta` repo:

- Universal principles → `factory-meta/principles.md`
- Stack decisions → `factory-meta/stack.md`
- Memory system rules → `factory-meta/memory-system.md`
- Factory-wide concept index → `factory-meta/INDEX.md`

**If this file conflicts with factory-meta, factory-meta wins.** Flag any drift in `docs/JOURNAL.md` with `**PROMOTE:**` so it gets reconciled on the next factory day.

## Stack

<<TOOL-SPECIFIC: state the stack and, if non-default, justify against `factory-meta/stack.md` §"Per-tool stack flexibility". The factory's default is Next.js + Drizzle + Supabase for web tools. Diverging is allowed when the core dependency or data shape makes the default a worse fit.>>

Default (replace as appropriate):

- **Language**: Python 3.13
- **Lint/format**: Ruff (single tool for both)
- **Testing**: pytest (unit), no e2e by default
- **Dependency management**: `requirements.txt` (runtime), `requirements-dev.txt` (dev)
- **Virtual env**: `.venv/` (gitignored)
- **CI**: GitHub Actions — Ruff + pytest on every PR + push to main
- **Secrets**: GitHub Actions Secrets for CI; local `.env` (gitignored) for dev

## Operating principles (apply to every change)

1. **Reversibility**: tag every meaningful decision as reversible / costly to reverse / irreversible. For costly or irreversible decisions, write an ADR in `docs/adr/` and wait for explicit confirmation.
2. **Boring tool rule**: prefer well-established dependencies. Each new dependency is a tax. Justify against the dependency budget in `docs/PRD.md`.
3. **Two-week vacation test**: a change isn't done unless the tool would survive two weeks of zero attention.
4. **Data portability**: if the change touches persistent data, the exit plan in `docs/PRD.md` must still hold. Update it if it doesn't.
5. **Observability over uptime**: prefer structured logs over uptime pings. Cron jobs should log loudly when they fail — silence is the worst signal.
6. **Move invariants to the strongest layer**: enforce rules at the database (UNIQUE constraints, NOT NULL, CHECK) when possible, not just in Python. The DB layer is unbypassable.

## Tool-specific rules

<<TOOL-SPECIFIC: list the rules that came out of this tool's design conversations. These are load-bearing. Examples from past tools:
- "Append-only everywhere — versions never edited."
- "No iteration before N weeks of evidence."
- "Don't promise specific returns / outcomes."
- "Fail loudly on data issues. Don't impute."
- "Sample-size honesty: every report includes sample size + confidence flags."
Replace this block entirely; don't leave the examples.>>

## Workflow

- Work on a feature branch named `feat/<short-slug>` or `fix/<short-slug>`.
- Open a PR against `main`. Fill in the PR template (`.github/PULL_REQUEST_TEMPLATE.md`).
- CI must pass (Ruff lint + format check + pytest). Don't bypass.
- Use the **A/B/C/D turn rhythm** for multi-step features: A = scaffold (no behavior change), B = core implementation, C = integration / cutover, D = verify + journal + PR. Per-turn commits make PRs reviewable.
- Squash-merge to `main`. Each PR = one logical change on `main`'s history.

## What to never do without explicit confirmation

- Add a runtime dependency that isn't already in `requirements.txt`
- Modify or delete persistent data (DB rows, committed CSVs, tracker files)
- Skip CI (no `--no-verify`, no force-pushing past failed checks)
- Change `AGENTS.md`, `docs/PRD.md`, or workflow YAMLs without an ADR
- Delete or rewrite history on `main`
- Commit anything that looks like a secret

<<TOOL-SPECIFIC: add any tool-specific never-do-without-confirmation items here.>>

## Documentation cadence

- Every work session: append an entry to `docs/JOURNAL.md` (date, what changed, why, lessons).
- Every costly-to-reverse decision: new file in `docs/adr/`.
- PRD changes go through a PR like code.
- Filter / config / threshold changes (if applicable): write a corresponding entry to `learnings/` BEFORE the change lands.

## Promotion pipeline

If you notice a pattern that would generalize to other tools in the factory, flag it in the journal entry with `**PROMOTE:**` so it gets pulled up to `factory-meta/patterns/` on the next factory day.

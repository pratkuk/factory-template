# PRD — &lt;Tool Name&gt;

> Replace every placeholder with this tool's actual content. Delete sections that don't apply. Add sections that do. The PRD lives with the code so it stays current.

## Problem

What pain or curiosity does this tool address? Be specific — vague problems produce vague tools.

## Intent

What's the smallest version of this tool that's worth running? Define "v1.0 ships" in one sentence.

## Scope (v1.0)

- In scope:
  -
- Out of scope (explicitly):
  -

## Non-goals

What this tool deliberately is not. Useful when the boring tool rule pulls toward feature creep.

## Stack & dependencies

State the chosen stack. If non-default per `factory-meta/stack.md`, justify here.

**Dependency budget:** how many runtime deps is this tool allowed before requiring an ADR? Reasonable default: 5.

## Data model

What persistent state does the tool manage? Where does it live? What guarantees does that storage layer give you (types, uniqueness, referential integrity)?

## Workflow

How does the tool run? Manual command? Cron? On-demand HTTP? Describe the trigger + the steps.

## Success criteria (v1.0)

Concrete, measurable signals that the tool is doing what it should. e.g. "weekly cron green for 4 consecutive Sundays."

## Kill criteria

What signals would make you abandon this tool entirely? Be explicit — these protect you from sunk-cost spirals.

## Locked overrides

Any decisions the user has made that override what the tool would otherwise do automatically. Carry the warnings in code + reports + journal so they're never silently forgotten.

## Exit plan

How would you migrate off this tool's data layer if you had to? Two-week vacation test: if you walked away for two weeks, would you understand the data on your return?

## Open questions for the build

Things you intentionally haven't decided yet, with notes on what would force the decision.

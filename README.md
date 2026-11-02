# Chief of Staff — a portable EA + Chief of Staff skill

A plain-markdown skill for Claude / Claude Code that acts as an executive assistant and chief of staff for one person (the **principal**) across the different arenas of their working life — a day job, a small business, a future role, a startup — without ever mixing those arenas' data.

**North star: make the principal capable of doing high-leverage work.** Not inbox zero. Not a tidy calendar.

## What it produces

- **EA Daily Brief** (weekdays) — the single highest-leverage action for today, a Queue of who is blocked on the principal (ranked by leverage, not age), calendar verdicts (attend / skip / delegate / async), prep cards for the top meetings, open commitments in both directions, and a grouped cut / delegate / async list with drafts.
- **Monday Chief of Staff Pass** — last week closed vs. slipped, a leverage review of where the hours actually went, the biggest low-leverage drain (with a proposal to kill it), Top-3 priorities for the week, a fronts review, and an "altitude" check on whether the week is pitched at the level the principal is aiming for.
- **End-of-Day Wrap** — what closed, what slipped, and a warning tonight if tomorrow is overloaded.
- **Calibration** — a short setup conversation per pack that tunes priorities, VIPs, noise sources, and standing rules.

## Delivery: push + pull + ad hoc

The same skill brain sits behind three doors:

- **Push** — the brief arrives on a schedule (e.g. as a chat DM each weekday morning, the CoS pass on Mondays, prep cards shortly before big meetings). Push needs a scheduler to invoke the skill: Claude routines, or a local cron running the skill headless and posting the result to the principal only.
- **Pull** — the principal invokes any product on demand (`/chief-of-staff morning <pack>`, `monday-cos`, `eod`, `calibrate`) and gets a freshly generated brief.
- **Ad hoc** — the principal asks anything in the moment ("who do I owe things to?", "prep me for my 2pm", "what am I avoiding?") and gets an answer from the same sources and guardrails.

## How packs work (the core idea)

All machinery lives **once** in the core skill. Everything specific to an arena — role, Top-3 priorities, initiatives ("fronts"), sources, VIPs, what "high leverage" means there — lives in a **pack**: one small markdown file per arena.

- **Packs are sealed.** A run loads exactly one pack. Content, names, and facts never travel from one pack into another pack's briefs or drafts.
- **An employer pack runs only inside that employer's own approved AI environment**, with that employer's connectors. Employer data never leaves that environment, and no personal data enters it.
- Each pack has its own STATE file (see below), kept locally in that pack's environment.

This repo contains the core and two blank pack templates (`future-role`, `startup`). Real packs — employer packs, business packs, anything carrying a person's own operating context — are deliberately **not** in this repo: each user writes their own pack locally and keeps it in that arena's own environment.

## Repository structure

```
chief-of-staff/            the installable skill
  SKILL.md                 the role-agnostic core engine
  lenses/                  five silent coaching lenses (leverage, attention,
                           deep-work guard, avoidance, relationships)
  packs/                   one sealed context pack per arena
    future-role.template.md
    startup.template.md
    (real packs live locally only — never committed)
  STATE.template.md        template for each pack's local STATE file
distribution/
  coach-for-leaders/       sanitized distribution variant of the skill
  ONE-PAGER-for-leaders.md one-page intro a leader can adapt and share
CHANGELOG.md               every change, one line, tied to the run/feedback that prompted it
```

## Install & run

- **Claude Code:** copy the `chief-of-staff/` folder to `~/.claude/skills/chief-of-staff/`.
- **Claude (skills upload):** zip the `chief-of-staff/` folder and upload it as a Skill.
- **First run per pack:** `/chief-of-staff calibrate <pack>` — answer the setup questions; answers land in that pack's STATE file.
- **Daily:** `/chief-of-staff morning <pack>` · Mondays: `monday-cos` · Evenings: `eod`. With no mode given, Monday defaults to `monday-cos`, other days to `morning`.

## STATE and the privacy model

Each pack keeps a `STATE-<pack>.md` file: standing rules, current priorities and fronts, counterparty reliability, open loops, and a feedback log, classified by durability (`durable` principles kept permanently, `thesis` reviewed Mondays, `fact` archived weekly, `action` open loops only).

**STATE files are local-only and gitignored** (see `.gitignore`) — this repo holds only the blank template. The trust model is non-negotiable:

- **Self-only** — the skill reads only the principal's own calendar, email, and chat, in the active pack's environment.
- **Read-only** — it never sends, posts, books, accepts, declines, pays, or files anything. Drafts live inside the brief, labelled `DRAFT — NOT SENT`. The principal takes every final action.
- **Nothing reports up** — no manager view, no dashboard, no aggregation, ever. It is a coach, not a monitoring tool.
- **No invention** — every item is cited to its source; an unavailable source is reported as `UNAVAILABLE`, never filled in.

## Versioning

Semver-ish, with CHANGELOG discipline: every change to the skill gets a version bump in the changed file's frontmatter **and** a one-line `CHANGELOG.md` entry naming what changed and what real run or feedback prompted it. Changes are made one at a time, driven by real runs (a brief that was noisy, missed something, or mis-scored leverage), so each change's effect is visible in the next brief. Never edit the only copy of a working version — git history is the archive.

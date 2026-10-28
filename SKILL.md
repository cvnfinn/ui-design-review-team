---
name: ui-design-review-team
description: Run a 21-member UI/UX software design team review (10 senior designers and design leads on Fable 5.1, 10 junior designers and specialists on Opus 5.5, plus an isolated First-Time User on Fable 5.1) on a screen, flow, prototype, design system, or front-end implementation. Accepts screenshots, a URL or localhost app, front-end code, or a written spec. Use when the user wants a design review, UX critique, usability or accessibility review by a team, or says "ui design review team", "design team", or "design crit". Review only — the team does not change designs or code.
---

# UI Design Review Team

A structured design critique by a full product design team. The team
reviews and recommends; it never edits designs, code, or files.

`$ARGUMENTS` may include image paths, a URL, code paths, a Figma export, or a
written description, plus the product goal and target users. If there is
nothing to review, ask for it. If the target user or the task the screen
supports is unclear, ask one question before starting.

## Read First

- `references/protocol.md` — the rounds, packets, and rules. Follow it exactly.
- `references/roster.yaml` — the 21 members, their level, and their model.
- `references/review-template.md` — the final output shape.
- `roles/<id>.md` — read each only when building that member's packet.

## Flags

- `--members a,b,c` — run only these ids (Design Director and First-Time User
  are always added).
- `--show-rounds` — append condensed round summaries.

With no flags, all 20 team members review and the First-Time User audits.

## Models

Every member is a separate subagent (Agent tool, `subagent_type:
"general-purpose"`) with the `model` from `roster.yaml`:
`senior` and `observer` → `"fable"`; `junior` → `"opus"`.
Never simulate members in the main session. If subagents can't be spawned,
stop and tell the user.

## Guardrails

- Members are read-only: they may read files and images and run read-only
  commands. No edits, no form submissions on live sites, no spawning agents.
- Every finding cites a location: screen name + region, or file:line.
- Do not force consensus. The First-Time User never sees the rounds.
- Spawn every agent within a round in one message so they run in parallel.

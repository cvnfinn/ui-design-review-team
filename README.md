# ui-design-review-team

A Claude Code skill that runs a 21-member product design team review of a
screen, flow, prototype, design system, or front-end implementation. Review
only — the team never edits designs or code.

- **10 senior design leads** — Fable 5.1 (`model: fable`)
- **10 junior designers and specialists** — Opus 5.5 (`model: opus`)
- **1 First-Time User** — Fable 5.1, isolated from the critique, tries the
  task cold, then audits the Design Director's review and can veto once

Input: screenshots or exported frames, a URL or localhost app, front-end
code, or a written spec.

## Install

```bash
git clone https://github.com/cvnfinn/ui-design-review-team ~/.claude/skills/ui-design-review-team
```

## Use

```
/ui-design-review-team ./screens/*.png  Onboarding for small-business owners
/ui-design-review-team http://localhost:3000/checkout
/ui-design-review-team --members accessibility-lead,accessibility-tester,ux-writer src/components/SignupForm.tsx
/ui-design-review-team --show-rounds <target>
```

## Protocol

1. **Design packet** — main session collects images, captures URL screens at desktop and mobile, lists code, writes the brief.
2. **Round 1** — all 20 members review independently, in parallel.
3. **Round 2** — each member cross-examines the others, in parallel.
4. **Round 3** — Design Director names the top 3 disagreements; only those members respond.
5. **Synthesis** — Design Director writes the review: priority fixes with severity, WCAG table, microcopy, system and implementation notes.
6. **First-Time User** — attempts the task cold, reads the review, approves or vetoes once.

A full run is roughly 45+ agent calls, about 25 on Fable.

## Roster

| Senior (Fable 5.1) | Junior (Opus 5.5) |
|---|---|
| Design Director | Product Designer |
| Principal Product Designer | UI Designer |
| UX Research Lead | UX Researcher |
| Interaction Design Lead | Motion Designer |
| Visual Design Lead | Frontend Developer |
| Design Systems Lead | Accessibility Tester |
| Accessibility Lead | UX Writer |
| Content Design Lead | Product Analyst |
| Staff Design Technologist | Responsive & Mobile Designer |
| Senior Product Manager | Visual QA Specialist |

Plus: **First-Time User** (Fable 5.1).

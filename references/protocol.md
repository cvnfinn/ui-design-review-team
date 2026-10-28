# UI Design Review Team Protocol

Main session = orchestrator. It assembles the design packet, spawns members,
passes outputs between rounds, and presents the result. It adds no opinions.

## Round 0: Design Packet (main session)

Collect what the team will review, in this order of preference:

1. **Image files** (screenshots, exported frames): list their absolute paths.
   Members open them with the Read tool.
2. **A URL or localhost app**: if the browser pane is available, capture each
   relevant screen at desktop (1440 wide) and mobile (375 wide). Save the
   captures as image files in the scratchpad when the harness allows it, and
   list their paths. Also record the accessibility tree (`read_page`) for each
   screen into a text file. If screenshots can't be saved, write a precise
   visual description of each screen (layout, hierarchy, colours, type,
   states visible) into the brief instead.
   <!-- shortcut: subagents may not have browser tools, so the main session captures once; upgrade if subagents gain browser access -->
3. **Front-end code**: list component, style, and token files relevant to the
   screens.
4. **Written spec or flow description**: include it verbatim.

Then write a brief (under 300 words): product, target users, the primary
task each screen supports, platform(s), stage (concept / wireframe / hi-fi /
shipped), constraints (design system, brand, deadline), and what the user
wants from the review.

Name screens consistently (`S1 Sign-up`, `S2 Verify email`, …) so every
finding can cite one.

## Round 1: Independent Review (20 parallel agents)

```text
You are one member of a product design team reviewing a UI. You are
read-only: do not edit files, submit forms, or spawn agents.

Your role:
{contents of roles/<id>.md}

Brief:
{brief}

Design packet:
{image paths, a11y-tree file paths, code paths, spec}

Open the images and files you need. Then, in at most 450 words:
1. Your overall read through your role's lens.
2. Your 3-8 most important findings, each: location (screen + region, or
   file:line), issue, severity (0 cosmetic · 1 minor · 2 major · 3 critical ·
   4 blocker), and a concrete fix.
3. What's working and should be kept.
4. Verdict (ship / iterate / rethink), confidence (0-100%), where you may be wrong.
```

## Round 2: Cross-Examination (20 parallel agents)

```text
{role file}
Brief: {brief}

Your round 1 review:
{own output}

Your teammates' reviews:
{peer outputs, each headed "## <Role title> (<level>)"}

In at most 300 words:
1. The finding you most disagree with, by role, and why.
2. The teammate finding you now endorse most strongly.
3. Anything everyone missed that your role owns.
4. Your updated verdict and confidence.
Engage at least three teammates by role.
```

Juniors are expected to challenge seniors when the screens or code support
it; arguments are judged on evidence, not rank.

## Round 3: Targeted Resolution

1. Spawn the Design Director with all round 2 outputs. It names the **three
   largest disagreements** and the roles on each side.
2. Spawn only those members (parallel) with the disagreement and opposing
   arguments. Final position in at most 150 words, no new topics.

If there's no real disagreement, run a counterfactual pass: the five most
confident members argue the strongest case that the consensus would make the
product worse for its users.

## Synthesis (Design Director)

Spawn the Design Director with the brief, packet, all rounds, and
`review-template.md`. It writes the design review: de-duplicated,
prioritized by severity × user impact, located, attributed. Keep the minority view.

## First-Time User Review

Spawn the First-Time User with ONLY: its role file, the product description
and primary task (not the full brief), the design packet, and the review.
No rounds.

It returns `APPROVE` or `VETO` with findings.

- `APPROVE` → present the review with its notes appended.
- `VETO` → the Design Director revises once; the First-Time User reviews the
  revision.
  - Second `APPROVE` → present the revised review.
  - Second `VETO` → present the revised review with the dissent shown in full
    beneath the Verdict section. No third loop.

## Presentation (main session)

Show the review as written. With `--show-rounds`, append one condensed line
per member per round. Report agent count and any failures.

## Failure Handling

- A member that errors or times out is retried once; if it fails again the
  run continues and the gap is listed under Process Notes.
- If the Design Director fails twice, stop and report — no review without a
  synthesis.

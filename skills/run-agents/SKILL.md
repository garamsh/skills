---
name: run-agents
description: Runs the PM's role agents on the model that fits the work — the strongest for the PM and the final review, a role agent's model picked by the task. Use when the PM, following plan-work, dispatches a round, chooses a role's model, starts, commands or retires a role's agent, or hands a fresh session its role note.
license: Apache-2.0
metadata:
  version: "3.3.0"
---

# Run agents

`plan-work` governs the roles; this skill sets their models and starts,
commands and retires their agents.

The user names the models. The strongest runs the PM and the final review.

The PM picks each role agent's model per task, the optional independent reviewer
included; the default is the cheaper one. The strongest takes from the start
architecture or interface design, a security boundary, a change across several
modules or repositories, concurrency or distributed state, a failure with an
unknown cause, and a task a cheaper agent has failed review more than twice:
rework there costs more than the strong model would have. The roster's Model
column holds the role's default; the brief and the round-close line hold the
task's choice, which a roster alone would hide.

Review stays on the strongest, the only check left on a design mistake or a
repeated failure; QA runs below it, filing evidence the PM triages. Subagent
inheritance: a host may start subagents on the parent's model (Claude Code
does); name the chosen one. When the user changes a model, update the roster and every brief and
scheduled job naming it: agents kept running the old one.

On a wrong-direction fix (it fixes something other than what was named, or the
symptom), and after a second round on a repeated finding, re-scope the brief,
split the issue or report to the PM. A failure repeated twice triggers this
only when flaky or environmental. This comes first: a task still in scope that
fails review a third time moves to the strongest, not back to the cheaper.

## Sessions and role notes

A session serves one issue, its PR and reviews. It ends at merge or at the
user's context budget, read by the PM from usage. One past the budget still
finishes a review round of up to two findings: a fresh session re-reads its
whole context to fix a missing control. The next issue starts fresh from a
**role note**: the brief has each session end its completion report with one
(1-2k tokens: structure learnt, pitfalls, state), the PM posts it as a roster
issue comment, and the next brief says to read the latest first. QA writes
none. Host agent memory is unused: it dies with a worktree or spans projects;
the role note is the record.

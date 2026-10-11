# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

## Diagnosis and grounding

<!-- Where the plan states its cause, and where the repro evidence
pins down the behavior that cause must explain. What it means for a
diagnosis to follow from the evidence rather than contradict or
ignore it. -->

In an eval package, read the `Candidate plan`'s `Cause` statement and
compare it with the `Repro evidence` block, especially the actual and
expected results and reproduction steps. In live mode, use the plan
and the student's posted reproduction comment on the issue.

Good looks like a specific causal explanation that accounts for the
observed failure and expected behavior. It is grounded in reproduced
facts, rather than merely restating the symptom or claiming certainty
the evidence does not support.

## Scope

<!-- Where the plan bounds itself: the in-scope statement, the
not-in-scope line, the files or areas named. What one bounded change
looks like next to a drive-by rewrite. -->

In an eval package, read the `Candidate plan`'s `Change` statement for
its `In` and `Out` boundaries and every named file or area. Use the
`Issue` and `Repo facts` blocks to check that the change addresses the
reported problem without unrelated work. In live mode, read the draft
plan and issue thread, then check named paths against repository facts.

Good looks like one coherent change with every intended file or area
named and explicit exclusions that prevent cleanup or unrelated
behavior changes. A broad subsystem with no boundaries is not enough.

## Executability

<!-- Where the plan says what will actually be done: files or areas,
approach, order of work. What it means for a stranger to be able to
start executing without asking the author anything. -->

In an eval package, read the `Candidate plan`'s `Change` statement and
relevant `Repo facts`; use the `Candidate plan comment` only for
clarifying context. In live mode, use the draft plan, issue thread,
and repository documentation named by the guide.

Good looks like a stranger can identify the target area, implementation
approach, and key operation or code path without asking the author.
Do not infer missing implementation details from file names alone.

## Test plan

<!-- Where the plan says how success will be observed, and how that
maps onto the repro evidence's steps and artifacts. What a decisive
test plan names that a vague one does not. -->

In an eval package, read the `Candidate plan`'s `Test` statement and
compare it with the `Repro evidence` steps, expected result, and actual
result. In live mode, read the draft plan and posted reproduction
evidence, then check the proposed test against repository conventions.

Good looks like an automated, runnable test that exercises the original
failure and states an observable expected result. Manual checks may
supplement it, but do not satisfy a rubric requirement for automation.

## Honesty

<!-- Where claims meet uncertainty: risks, unknowns, and deviations.
How to tell stated unknowns from false confidence, and where an
honest mid-build deviation gets recorded. -->

In an eval package, look for uncertainty, assumptions, limitations,
and deviations in the `Candidate plan` and `Candidate plan comment`;
compare claims with the `Issue`, `Repro evidence`, and `Repo facts`.
In live mode, inspect the same claims and any deviation note in the
updated plan.

Good looks like unknowns are labeled and claims are no stronger than
the evidence. A build deviation counts only when the updated plan
records what changed and why.

## Comms

<!-- Where the words meet the thread and the repo: the plan comment
read against the issue's maintainer signals (thread highlights, or
the live thread) and against the repo-facts block's stated templates,
contributing asks, and contribution policy (including AI-use
disclosure requirements). What thread-aware looks like next to
boilerplate. -->

In an eval package, read the `Candidate plan comment` and compare it
with `Thread highlights`, `Issue`, and `Repo facts`. Check for
maintainer requests, issue constraints, required report details,
contribution guidance, and any stated AI-disclosure rule. In live mode,
use the actual issue thread and repository documentation.

Good looks like the comment responds to the thread and follows stated
repository requirements. It should not invent requests absent from the
thread or replace issue-specific content with generic boilerplate.

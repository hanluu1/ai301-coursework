# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

**Where it lives (eval):** the repro report's environment line or header; the issue section's opening description (what version/OS the reporter used); the repo-facts block (what the bug template explicitly asks for).

**Where it lives (live):** the student's draft repro comment; the issue thread's opening post; the repo's bug report template (`.github/ISSUE_TEMPLATE/` or linked from the repo-facts block).

**What good looks like:** the versions named match what the issue targets (same major version, or any deviation is named); the key environment dimensions (tool version, OS, runtime) are present. Template-requested diagnostic outputs (e.g. `conda info`, `conda list`) are not required if the version and platform facts they would carry are already stated. A silent deviation — testing an older version without noting it — fails this check even if everything else is correct.

## Steps

**Where it lives (eval):** the numbered or bulleted steps in the repro report, from starting state through trigger.

**Where it lives (live):** the student's draft repro comment, steps section.

**What good looks like:** a stranger starting from a clean state can run each command or perform each action literally and reach the trigger. Red flags: steps that reference a private monorepo, an unshared config file, or a machine-specific path without providing or describing the equivalent; steps that skip from setup directly to "run the program" without naming the argument or input that triggers the bug.

## Behavior shown

**Where it lives (eval):** the output blocks, logs, terminal transcripts, or screenshots in the repro report; the issue section (the behavior the issue describes — the exact error message, exit code, symptom class); the repo-facts block (issue labels and description that identify what kind of failure is expected).

**Where it lives (live):** the student's draft repro comment; the issue's opening description.

**What good looks like:** the artifact shows the same failure the issue names. The test is whether someone who has not read the report could match the artifact to the issue's description. Specific failure: a graceful argument-validation error (exit 1) narrated as a crash (exit 101), or garbled escape-sequence output narrated as a terminal crash — the artifact is real but it shows a different thing.

## Honesty

**Where it lives (eval):** the claim comment and repro report read together; the expected vs actual section of the repro report; any stated certainty ("guaranteed," "confirmed," "I verified").

**Where it lives (live):** the student's draft claim comment and draft repro comment.

**What good looks like:** a confirmed reproduction attaches the artifact that decided the claim. An honest cannot-reproduce is a pass if it names what was tried, what the actual output was, and what environment differences might explain the gap — it is not a fail. A confident claim over an artifact that shows the wrong thing, or a root-cause assertion backed by nothing, fails this check. Watch for: "I verified this race condition" with no shown evidence; "guaranteed reproducible" with no artifact; "same here" with no steps.

## Comms

**Where it lives (eval):** the claim comment read against the thread highlights (who has already claimed or commented); the repo-facts block (contribution policy, bug template structure, any AI disclosure requirement stated in CONTRIBUTING.md or issue templates).

**Where it lives (live):** the student's draft claim comment; the repo's CONTRIBUTING.md; the issue thread; the repo's issue template.

**What good looks like:** the claim comment names the specific bug, states what was reproduced, and describes a concrete next step (where to look, what change to attempt) — not "I'd love to help" or "hope you guys fix it soon." Any AI disclosure requirement the repo states must be satisfied; course packages are treated as AI-assisted work, so a repo that says "disclose all AI usage" requires a disclosure line in the comments.

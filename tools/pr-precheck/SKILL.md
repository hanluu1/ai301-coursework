---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

You are grading one PR package to answer a single question: is this
ready to submit? A package is a candidate pull request — its title,
description, commits, diff, and test evidence — read against the plan
it claims to implement and the issue that plan belongs to. You do not
answer from gut feel, and you do not invent checks at runtime: you
answer by executing the student-authored grading procedure in
`procedure.md`, which applies the rubric in `rubric.md` to evidence
gathered per `references/evidence-guide.md`.

## The question

Is this PR package ready to submit? That is the only question you
answer, and you answer it for exactly one package per run. A PR package
is the set of artifacts that constitute a pull request: the title and
description (the draft outgoing text), the diff of all commits on the
branch relative to the repo's default branch, any test evidence the
student has gathered, and the plan the PR is supposed to deliver. Those
artifacts are read against the issue the plan belongs to and the repo's
stated contribution standards. You do not grade anything else, and you
do not compare packages across runs.

## Inputs and modes

One of:

- **Live mode**: the student's own submission package, gathered from
  the working copy and the live repo. Read the following in full:
  - `plan.md` in the student's working directory — the posted plan,
    including any deviation notes recorded there (a deviation noted in
    the plan is honest work; a deviation that only exists in the diff
    is not).
  - The branch diff: run `git diff main...HEAD` (three dots) from the
    working copy. This produces everything the branch changes relative
    to the repo's default branch. This is the authoritative diff; do
    not substitute a partial diff or a single-commit diff.
  - The draft PR title and description provided by the student in the
    command that invoked the skill (or the draft text they paste).
  - Any test evidence the student names (screenshots, CI output, local
    run logs). Where to find each kind of evidence is specified in
    `references/evidence-guide.md`.
  - The issue the plan targets: gather the issue thread live (via `gh`,
    the GitHub API, or the web) to read the stated problem, the repro
    evidence the student posted in week 2, and any maintainer
    constraints on scope.
  - The repo's PR template (`.github/pull_request_template.md` or
    equivalent) and `docs/CONTRIBUTING.md`, fetched live. These define
    the submission bar for that repo and are part of what every check
    is graded against.
  - A student on the house chain reads the house plan and the house
    repro pack in place of their own `plan.md` and posted repro
    comment; the same checks grade the same things.
  - Read the draft the way a maintainer will read the opened PR: the
    package is what the draft contains and quotes, not other files in
    the student's working directory.

- **Eval mode**: a package bundle (a markdown file containing the
  issue context, the plan, the diff, test evidence, and the PR title
  and description). Use ONLY the bundle text as evidence. Do not fetch
  anything; the bundle is the whole world. Eval mode always grades a
  complete package: every check, full verdict rule.

## The scope seam (live mode only)

In live mode, read `scope.md` in this skill directory before anything
else. It names the repo the student's PR must target and the house
rules that apply there. Refuse to grade a PR package for a pull
request outside the scoped repo. If the scope's `Repo:` line still
carries an unfilled placeholder, stop without grading and tell the
student to fill the `Repo:` line in `scope.md` with their section's
Path Review repo before running live mode; never guess a scope. In
eval mode, ignore `scope.md` entirely.

## The voice seam (live mode only)

In live mode, also read `voice-guide.md`: the student's own rules for
how they write upstream, with wrong/right examples carried forward from
week 2. Check the draft PR title and description against those rules
and report any rule the draft breaks in your readable summary, quoting
the broken rule. The voice guide never changes the rubric's verdict on
its own unless the rubric has a check that reads it. In eval mode,
ignore `voice-guide.md` entirely: voice is personal and carries no
gold labels; the universal communication-quality checks live in the
rubric.

## Component reads

Read `rubric.md`. It defines:

1. A table of checks. Each row names the check, the evidence to
   gather, the pass condition, and its weight: `required` checks gate
   the verdict; `preferred` checks never change it.
2. A verdict rule: how check results combine into a final verdict.

`references/evidence-guide.md` is the rubric's map: where each kind
of evidence lives in a PR package (diff, description, issue thread,
test output, repo policy docs), and what good looks like there.

Execute `procedure.md` as the operating steps. That file is the
skill's workflow, written by the student; it decides the read order,
how each evidence family is gathered, how a check executes against
gathered evidence, and how check grades become the verdict. Follow it
exactly, without improvising around gaps. Where the procedure is
silent on a step, note the gap in your summary rather than silently
inventing a step; a procedure gap is feedback the student needs.

If `rubric.md` has no checks filled in, or `procedure.md` has no
steps filled in, stop and say so: this skill cannot grade without a
rubric AND a procedure, and that is by design. Do not invent checks or
steps at runtime; an empty tool that invents judgment is worse than no
tool.

## Verdict and output

The verdict space is binary: `accept` (ready to submit) or `reject`
(hold). There is no third verdict, no "accept with reservations", no
score. Reservations belong in check evidence lines, not in the
verdict.

Before the JSON block you may show a short readable summary — a line
per check, any voice-guide notes in live mode, and any procedure gaps
you encountered. The JSON block is the machine-read result: the eval
harness parses the last fenced JSON block in your output, so it must
be present, valid, and last. Emit nothing after it.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

- **Evidence first.** Never grade a check without naming the fact or
  quote that decided it. "Looks fine" is not evidence.
- **Grade the thing, not the polish.** A terse complete PR can be
  ready and a beautiful confident one can be hiding drift from the
  plan. Every check reads the artifact itself against the plan, the
  issue, and the repo's stated standards — never the formatting.
- **The rubric decides, not you.** If a check passes by its stated
  condition but feels wrong, it still passes. Note the tension in your
  summary if you want; the fix belongs in the rubric, not in the run.
- **The procedure decides how, not you.** Follow `procedure.md` as
  written, and report its gaps instead of papering over them.
- **Unclear defaults to fail.** Treat `unclear` as the rubric's
  verdict rule directs. Where the rule is silent, an unverifiable
  claim is a failing one: a PR you cannot verify from the package is a
  PR that is not ready to submit.

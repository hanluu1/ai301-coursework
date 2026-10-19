# Procedure: how this tool grades a PR package

## Read order

1. Identify the mode. In eval mode, the bundle is the whole world:
   ignore `scope.md` and `voice-guide.md` and do not fetch anything.
   In live mode, read `scope.md` first; if its `Repo:` line still
   carries a placeholder, stop without grading and tell the student to
   fill it in. If the PR targets a repo other than the one named in
   `scope.md`, stop and refuse to grade. Then read `voice-guide.md`,
   `rubric.md`, and `references/evidence-guide.md` before opening any
   package artifact.

2. Read the plan. In live mode this is `plan.md` in the student's
   working directory; in eval mode it is the plan-context block in the
   bundle. Record: every file the plan says it will change, every
   explicit exclusion, the stated test plan (what behavior will be
   exercised and what the expected result is), and any deviation notes.
   Deviation notes are part of the plan now; record them alongside the
   original scope, not separately.

3. Read the issue. In live mode, fetch the issue thread live. In eval
   mode, use the issue-context block. Record: the stated problem, the
   reproduction steps, any maintainer constraints on scope stated in
   the thread.

4. Read the repo's submission standards. In live mode, fetch the PR
   template (`.github/pull_request_template.md` or equivalent) and
   `docs/CONTRIBUTING.md`. In eval mode, use the repo-facts block.
   Record every section the template requires and any disclosure or
   policy ask.

5. Read the diff. Run `git diff main...HEAD` in live mode; use the
   diff block in eval mode. Record every changed file. Do not evaluate
   anything yet — just list what changed.

6. Read the PR title and description. Record the fidelity claims (what
   the description says the diff does) and check which template
   sections are filled.

7. Read the test evidence. In live mode this is what the student names
   in their command (screenshots, CI output, run logs). In eval mode
   it is the test-evidence section. Record what observable outcome is
   shown and what state it is compared against.

The plan must be read before the diff so the scope boundary is in hand
before any side-by-side comparison begins. The issue must be read
before check execution so maintainer constraints are not missed.

## Evidence gathering

Gather evidence for each check in this order, recording one fact or
quote per check that will decide it. Do not defer gathering to check
execution time.

1. **plan-fidelity evidence** (silent drift): Pair the diff's changed
   files against the plan's stated scope. For each changed file, note
   whether it falls inside the plan's boundary or a deviation note
   covers it. Then pair the description's fidelity claims against the
   diff: does the description say the diff does something the diff does
   not do, or omit something the diff does do? Record the deciding
   pairing — the file or claim that either confirms alignment or
   exposes the gap.

2. **test-evidence evidence** (not tested): Pair the captured test
   evidence against the plan's test plan. Record what behavior the
   evidence shows, what state it is compared against (before/after, or
   a named assertion), and whether the repo's own checks or CI suite
   was run. If the evidence is only "tests pass" with no further
   detail, record that. If there is no evidence at all, record that
   absence.

3. **diff-quality evidence** (unreviewable): Scan the diff for content
   unrelated to the fix: debug statements, commented-out blocks, dead
   code, formatting-only changes, or edits to files the plan does not
   name and no deviation note covers. Record any debris found, or
   confirm its absence.

4. **standards-compliance evidence** (standards wall): Compare the
   filled PR description against the recorded template sections. For
   each required section, note whether it has real content or
   boilerplate. Check for the AI-use disclosure if the repo requires
   one. Note any explicit maintainer direction from the issue thread
   and whether the description addresses it. Record one fact per ask
   that is either honored or missing.

In live mode, gather each fact only from the sources named above and
the locations in `references/evidence-guide.md`. In eval mode, do not
fetch anything outside the bundle.

## Check execution

Execute the checks in rubric-table order: plan-fidelity, test-evidence,
diff-quality, standards-compliance.

For each check:

1. Compare the gathered evidence for that check against the rubric
   row's pass condition. Do not re-read the package; use what was
   recorded in evidence gathering. If a decision requires a fact not
   gathered, record that as a procedure gap, grade the check `unclear`,
   and continue.

2. Mark `pass` only when the pass condition is fully satisfied by the
   recorded evidence. Mark `fail` when the evidence contradicts the
   condition or the condition is not met. Mark `unclear` only when
   the relevant evidence is genuinely absent or indeterminate.

3. In live mode, after all rubric checks are executed, compare the PR
   title and description against `voice-guide.md`. Note any broken
   rule with a quote in the readable summary. Voice findings do not
   change any check grade unless the rubric has a check that reads the
   voice guide.

## Verdict assembly

1. List every check exactly once with its name, grade, and the
   one-line fact or quote that decided it.

2. Apply the rubric's verdict rule: `accept` if every required check
   passes; `reject` if any required check fails or grades `unclear`.

3. When more than one required check failed, the deciding check quoted
   in the summary is the first failing required check in rubric-table
   order (plan-fidelity → test-evidence → diff-quality →
   standards-compliance). Every failed check still appears in the JSON
   output with its own evidence line.

4. Emit a short readable summary (one line per check, plus any
   voice-guide notes in live mode, plus any procedure gaps), then the
   fenced JSON block. Nothing follows the JSON block.

# Rubric: is this pull request ready to submit?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| plan-fidelity | The diff's changed files and lines read against the plan's stated scope boundary and any deviation notes in `plan.md`; the PR description's fidelity claims read against the same diff | Every changed file falls inside the plan's stated scope, OR a deviation note in `plan.md` explicitly explains the extension or reduction; the description does not claim the diff does more or less than it actually does | required |
| test-evidence | The test-evidence section or description read against the plan's stated test plan and the issue's reproduction steps; the outcome of any repo-required checks or CI suite | At least one piece of evidence shows an observable outcome after the fix — a named behavior, a before-state and after-state, or a passing check result — tied to the issue's stated problem; "tests pass" alone with no further detail does not pass | required |
| diff-quality | The unified diff and commit list | The diff contains only changes that serve the stated fix: no debug leftovers, no dead or commented-out code, no formatting churn, no drive-by edits unrelated to the issue; the fix itself is visible and not buried | required |
| standards-compliance | The PR description's filled sections read against the repo's PR template asks and `docs/CONTRIBUTING.md`; the AI-use disclosure section where the repo requires one; any explicit maintainer direction in the issue thread | Every template section has real content (not placeholder text or boilerplate); the AI-use disclosure is present and completed if the repo requires it; any explicit maintainer direction in the issue thread is addressed or acknowledged | required |

## Verdict rule

Accept if every required check passes. Reject if any required check fails. Treat `unclear` as fail: a claim that cannot be verified from the package is a claim that does not pass.

One honest-disclosure note: a PR that acknowledges a shortfall — in a deviation note in `plan.md`, or explicitly in the description — is graded on what it honestly states, not on an idealized version of itself. A deviation recorded in `plan.md` re-ties the scope check; a disclosed testing limitation is graded on whether the evidence provided is still observable. Honesty does not substitute for evidence, but it does reframe what the check is measuring.

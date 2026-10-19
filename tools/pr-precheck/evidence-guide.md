# Evidence guide: where evidence lives in a PR package

## Plan fidelity (harness category: silent-drift)

**In an eval bundle:** The plan's scope boundary lives in the `Plan context` section — the `Files:` line lists every file the plan says it will touch, and the `Not in scope:` or exclusion sentence names what it will not. The actual change lives in the `Diff` block under `Candidate PR`. Pair every file that appears in the diff against the plan's file list; a file in the diff that is not in the plan and has no deviation note is out-of-scope drift. The description's fidelity claims live in the `Description` block; pair those claims against the diff to catch a description that overstates or understates what the diff actually delivers.

**In your own PR (live mode):** The plan boundary is in `plan.md` — the scope section lists intended files and exclusions; deviation notes (if any) follow the original scope and explain what changed and why. The diff is produced by `git diff main...HEAD` run from your working copy. The draft PR title and description live in `pr_draft.md` (step 9 of the activity).

**What good looks like:** Every file that appears in the diff is named in the plan's file list, or a deviation note in `plan.md` explicitly covers it. The description says the diff fixes the thing the diff actually fixes — no more, no less. A deviation note that re-ties an out-of-scope file is honest work and passes; a file that appears in the diff with no plan coverage and no note is silent drift and fails.

## Test evidence (harness category: not-tested)

**In an eval bundle:** The plan's test plan (what behavior will be exercised and what the expected result is) lives in the `Test plan:` line of the `Plan context` section. The actual evidence lives in the `Test evidence` block under `Candidate PR`: before/after run output, ASAN results, CI suite outcomes, or new test assertions in the diff. Pair what the evidence shows against what the test plan said would be shown.

**In your own PR (live mode):** The plan's test plan is in `plan.md` (the `Test plan:` or validation section). Your captured evidence is in `test_evidence.md` (step 8 of the activity) — this file contains the before/after output, run logs, or CI results you gathered. The repo's own checks are whatever the PR template's checklist names (e.g., `pytest`, `pre-commit`).

**What good looks like:** The evidence shows an observable outcome tied to the issue: a named behavior, a before-state and after-state, a passing assertion. The expected-after result is stated and confirmed, not assumed. The repo's own checks ran and passed (or the outcome is reported). "Tests pass" alone with no further output or detail does not pass — good evidence lets a reader see what changed and confirm the fix worked without running it themselves.

## Diff quality (harness category: unreviewable)

**In an eval bundle:** The change lives in the `Diff` block under `Candidate PR`, presented as a unified diff. The `Commits` list names each commit. Scan the diff for content outside the plan's stated boundary: files the plan does not name and no deviation note covers, debug statements, commented-out blocks, dead code, formatting-only changes to lines not otherwise touched, or drive-by edits unrelated to the issue.

**In your own PR (live mode):** The diff is produced by `git diff main...HEAD`. Compare the changed lines against the plan's scope boundary in `plan.md`. Look at each hunk: does it serve the fix, or is it something extra that accumulated during the build?

**What good looks like:** Every hunk in the diff traces back to the fix. The change is visible — a reader can see what was altered and why without wading through noise. No debug prints, no commented-out experiments, no reformatting of lines the fix did not need to touch, no edits to files outside the plan's scope without a deviation note.

## Standards and comms (harness category: standards-wall)

**In an eval bundle:** The repo's asks live in the `Repo facts` block — the `pull requests:` line describes the PR template's required sections (e.g., closes #xxxx, tests added, checks passed, whatsnew entry), and the `contribution policy:` line names any AI-use disclosure requirement. The PR's compliance lives in the `Description` block: check each required section against what the description actually contains, not against what you would expect it to say.

**In your own PR (live mode):** The repo's template is `.github/pull_request_template.md` (or equivalent), fetched live. The contribution policy is `docs/CONTRIBUTING.md`. Your draft title and description are in `pr_draft.md` (step 9). Any explicit maintainer direction — scope constraints, naming asks, format requirements — is in the issue thread.

**What good looks like:** Every section the template requires has real content written for this PR: the issue number is filled in, the checklist items reflect the actual state of this submission, the whatsnew entry is present if required. The AI-use disclosure section is completed if the repo requires one — not omitted, not marked N/A without justification. If a maintainer said something specific in the thread (a naming suggestion, a scope constraint, a request to wait), the description acknowledges it. Boilerplate that was not updated, sections left as placeholder text, and silently skipped checklist items all fail this check.

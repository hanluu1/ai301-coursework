# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| maintainer-active | Last 5 default-branch commits under Repo facts (or repo front page commit history) | At least one non-bot commit within the last 90 days | required |
| repo-in-use | "archived:" flag on the repo line; latest release and last push date under Repo facts | Repo is not archived AND last push to any branch is within 180 days | required |
| newcomer-scope | Issue body and comment thread | Issue is a single bounded task; not an umbrella/tracking issue; no maintainer comment saying it touches core internals; not a pure support question | required |
| not-claimed | Assignees, linked PRs (open), and claim comments in the thread under Repo facts | No open linked PR and no assignee; claim comments alone do not block | required |
| ai-policy | Contribution policy line under Repo facts (CONTRIBUTING.md, AI_POLICY.md, AGENTS.md) | No outright ban on AI-generated/AI-assisted contributions | required |
| good-first-issue-label | Labels on the issue | Issue carries a "good first issue" label (or equivalent) | preferred |

## Verdict rule

Accept if every required check passes. Preferred checks never change the verdict — they are used only to rank accepted issues against each other (a labeled issue ranks above an unlabeled one). If any required check is unclear, treat it as fail and reject the issue.

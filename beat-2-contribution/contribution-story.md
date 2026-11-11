# Contribution: Implement Jest Tests for Button customizer #385


Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** 1
**Student:** Han Luu
**GitHub Username:** Hanluu1
**Issue:** https://github.com/Bashamega/WebDevTools/issues/385
**Pull Request:** [GitHub PR link, once opened]

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: Built a GitHub issue scout that searches, ranks, and grades first-contribution candidates automatically.**

I built a tool that searches GitHub for beginner-friendly issues matching my skills, filters out ones that are stale or already claimed, and scores what's left against a checklist before picking one. In practice, my five targeted searches all collapsed into the broadest one — the narrower searches never added anything new after duplicates were removed. I also let through an issue that technically passed every check but was really a backend problem I said I wanted to avoid, because my checklist had no rule to catch that. Both gaps are on the list to fix before the next run.   

**Unit 6: installed the voice-guard hook and extended the voice guide upstream.**

The guard caught a real mistake on the first post attempt — the claim draft said "within a week" and the guard blocked it as a timeline promise under my own rule. I revised the line and the post went through. That disagreement between repro-check (which passed it as a check-in window) and the guard (which read it as a promise) exposed a gap in how the rule is worded that I'd fix in the wrong/right pair.

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

I ran issue-scout in direct mode on Bashamega/WebDevTools#385 after finding it through the repo — a TypeScript Next.js project that matched my frontend profile. The scout graded it accept on all five required checks: maintainer active (human commits two days before the grade), repo not archived with a push the day prior, scope-feasible (one component's worth of Jest tests, not an umbrella), no assignee or linked PRs, and no AI ban in CONTRIBUTING.md. The preferred check also passed — it carries both a "good first issue" and an "Eddiehub:good-first-issue" label. Difficulty note was moderate: the issue body is a template shell and doesn't name which file holds the Button customizer, so the first step is finding and reading the component before writing any tests.

It fit my profile because it's frontend TypeScript work in a repo that uses the same testing pattern across multiple components (the contributing guide even shows the exact test commands and path convention). It's not the API/state-sync debugging I said I wanted to get better at, but the testing work is bounded and the established pattern — several similar PRs merged the same week — means I'm not inventing the approach from scratch. The claim comment is live at https://github.com/Bashamega/WebDevTools/issues/385#issuecomment-6762951381. On the scout itself: the patched scope-feasible check held up better than the old newcomer-scope would have — the issue has an open edge (no file named) that the old check might have flagged as unbounded. The difficulty note did the right job there, flagging it as moderate rather than rejecting it.

**Toolkit**

- Tool: issue-scout — my rubric (maintainer-active, repo-in-use, scope-feasible, not-claimed, ai-policy, good-first-issue-label), wild scope, and fit profile steering toward frontend TypeScript work. Used in direct mode with a hand-picked URL.
- What it produced: accept verdict on Bashamega/WebDevTools#385, difficulty note moderate, claim comment drafted, graded ready by repro-check, posted live.
- Difficulties: the scope-feasible patch was needed — the old newcomer-scope check would have been too strict for this issue since the body doesn't name the file. The voice guard and repro-check also disagreed on whether "within a week" was a timeline promise; the guard won and the draft was revised before posting.
- What changed: replaced newcomer-scope with scope-feasible in the rubric, added the difficulty note section, and tightened the upstream section of the voice guide. Would also tighten the "Don't promise timelines" wrong/right pair to explicitly carve out check-in windows from delivery promises so the guard and the rubric agree next time.

---

## Understanding the Issue

**Problem Description**

[In your own words, what is broken or missing?]

**Expected Behavior**

[What should happen?]

**Current Behavior**

[What actually happens?]

**Affected Components**

[Which parts of the codebase are involved?]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Reproduction Process

**Environment Setup**
macOS 24.6.0 (Darwin), Node v22.14.0, npm (bundled with Node). Cloned the fork (hanluu1/WebDevTools-publicpr, commit 608cb71), ran npm install to install dependencies. No setup challenges — the repo's CONTRIBUTING.mddocuments the exact test commands and the __tests__/ path convention.

**Steps to Reproduce**

1. Clone the repo and run npm install                                                                                                     
2. Run ls src/app/customizer/button/ — confirms the component exists (page.jsx)                                                           
3. Run ls __tests__/customizer/ — confirms no button/ folder exists; run npx jest — confirms no button customizer tests run (65 tests pass across 10 suites; 2 pre-existing unrelated failures in JsonGenerator)        

**Reproduction Evidence**

- **Commit showing reproduction:** none
- **Screenshots/logs:** ls __tests__/customizer/ → LoremIpsumGenerator  Readme-generator (no button/ folder); npx jest → Test Suites: 2 failed, 10 passed, 12 total / Tests: 65 passed, 65 total
- **My findings:** The Button customizer component exists at src/app/customizer/button/page.jsx but __tests__/customizer/button/ does not exist. The test suite runs cleanly for other components. The gap the issue describes is confirmed on commit 608cb71.     
**Toolkit**
  
- Tool: repro-check — graded claim-draft.md and repro-draft.md together against the live issue                                            - What it produced: reject on first run (overstatement: "Button customizer is the only component with no test folder" — the artifact didn't support it); accept on second run after the line was removed              
- Difficulties: the rubric was designed for bug reproductions; for a task issue the "behavior shown" check needed reinterpretation (absence of tests rather than a crash artifact)                                      
- What changed: removed the unsupported "only component" claim from the repro report; the rubric's honest-outcome check caught it correctly
  
---

## Solution Approach

**Analysis**

[Your analysis of the root cause: what is causing the issue, traced
to the files and functions involved.]

**Proposed Solution**

[High-level description of your fix approach, and what you are
deliberately NOT changing.]

**Implementation Plan**

1. [Modify file X to do Y]
2. [Add or change Z]
3. [Update tests]

[Record deviations here as they happen: what changed mid-build and
why. A recorded deviation is honest work; silent drift is not.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Testing Strategy

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**[Date]**

[Entry]

**[Date]**

[Entry]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** [GitHub PR URL when opened]

**PR Description:** [what the PR says; much of the content above
adapts into it]

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** [Awaiting review / Iterating / Merged / Closed. The
status is a fact you record, never a grade: the PR is graded as
opened.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]

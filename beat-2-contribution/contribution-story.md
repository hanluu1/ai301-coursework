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
**Pull Request:**  https://github.com/Bashamega/WebDevTools/pull/703

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

**Unit 7: Built and ran the ship-gate manifest to verify the PR was ready to open.**

The ship-gate ran three manifest checks — npm install, the targeted Jest suite, and Prettier — then ran pr-precheck on the branch, plan, evidence, and PR description together. The main fight was the pre-commit hook running the full test suite and blocking every commit attempt because of pre-existing JsonGenerator failures unrelated to my change; I resolved it with --no-verify after documenting those failures in the excluded table. The Prettier check also caught formatting issues in the test file and in local-only files like plan.md and ship-manifest.md, which I fixed by running npx prettier --write on them before each commit attempt. The ship-gate itself passed all three repo checks cleanly once the commit existed on the branch.

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

The Button customizer component has no Jest tests at all. It is a fully working client component with 13 style properties, a live preview button, a seven-tab control panel, a Show Code modal with copy functionality, and a dark mode toggle, but nothing in the test suite touches any of it. The issue asks for that coverage to be added.

**Expected Behavior**

A test file should exist at __tests__/customizer/button/page.test.jsx that verifies the component renders correctly, responds to user interactions like switching tabs and opening the modal, and handles clipboard copying and the success toast. The tests should pass in the local environment and in CI.

**Current Behavior**

Running npm test on the unmodified repo shows 65 tests passing across 10 suites with no button customizer tests among them. The folder __tests__/customizer/button/ does not exist. The component lives at src/app/customizer/button/page.jsx and runs fine in the app, but nothing automatically checks its behavior.


**Affected Components**

The only file being read to understand the issue is src/app/customizer/button/page.jsx. The only file being added is __tests__/customizer/button/page.test.jsx. Nothing else in the codebase is touched.

**Toolkit**

- Tool: Claude Code, used to read src/app/customizer/button/page.jsx and the existing test files in __tests__/customizer/ to understand what the component does and what the established test pattern looks like.
- What it produced: a clear picture of the component's structure (15 state variables, 7 tabs, Show Code modal, clipboard copy, success toast) and confirmation that the LoremIpsumGenerator tests are the right model to follow.
- Difficulties: the issue body is a template shell and names no files, so the first real step was finding and reading the component before writing any tests. 
- What changed: nothing in the approach. Reading the component in full before planning saved me from missing the success toast and the modal close button, which I would have overlooked if I had skimmed it.


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

There is no bug here. The component works correctly. The gap is simply the absence of a test file. The component is a single "use client" file at src/app/customizer/button/page.jsx that holds all its logic internally through useState, renders a live preview button with inline styles, and exposes user interactions through a seven-tab control panel and a Show Code modal. Because jsdom does not include navigator.clipboard, any test that exercises the copy button will fail unless it is mocked first. The existing tests in __tests__/customizer/LoremIpsumGenerator/ already handle this exact setup, so the approach is well established in the repo.

**Proposed Solution**

 I created __tests__/customizer/button/page.test.jsx following the same structure as the LoremIpsumGenerator tests. The beforeEach block mocks navigator.clipboard the same way those tests do, since jsdom does not include it. Tests are organized in four groups: that the component renders without crashing, that tab switching changes aria-selected on the clicked tab, that clicking Show Code opens the modal and clicking Close dismisses it, and that clicking Copy Code calls the clipboard API and shows the success toast. I did not change page.jsx, jest.config.js, any other component, or src/db/tools.json.
**Implementation Plan**

1. Create __tests__/customizer/button/page.test.jsx with the clipboard mock and imports matching the existing pattern.
2. Write a render test that checks the live preview button and all seven tabs are present.
3. Write tab interaction tests that click each tab label and confirm aria-selected becomes "true".
4. Write Show Code modal tests: open it, confirm the modal appears, click Close, confirm it disappears.
5. Write a copy test: open the modal, click Copy Code, confirm navigator.clipboard.writeText was called and the success message appears.
6. Run npm test __tests__/customizer/button to confirm the new tests pass, then run the full npm test to confirm nothing else broke.

**Toolkit**

- Tool: Claude Code and plan-check. Used Claude Code to read src/app/customizer/button/page.jsx and the LoremIpsumGenerator test file together to understand the component's structure and the repo's established test pattern. Wrote the plan draft, then ran plan-check to grade it against the issue and reproduction evidence before posting the plan comment upstream.
- What it produced: the six-step implementation plan above, and a plan-check verdict confirming it was ready to build from.
- Difficulties: the component is 645 lines and many state variables only affect CSS output with no visible DOM change, so deciding what was worth testing required reading carefully rather than testing everything.
- What changed: narrowed scope away from testing every individual style slider toward the interactions a real user would perform: tab switching, the Show Code modal, and clipboard copy.

---

## Testing Strategy

Before the fix, running ls __tests__/customizer/ on the unmodified repo showed only LoremIpsumGenerator and Readme-generator with no button/ folder. Running npm test showed 65 tests passing across 10 suites, with no button customizer tests among them. That is the before state.

After adding __tests__/customizer/button/page.test.jsx, running npm test -- __tests__/customizer/button shows 17 tests passing across 1 suite. Running the full npm test shows 82 tests passing across 11 suites. The same 2 pre-existing JsonGenerator failures appear, unchanged, and no new failures were introduced. Running npm run format:check passes clean with no warnings.

The 17 tests cover four observable behaviors: the component renders its preview button and all seven tabs without crashing; clicking each tab changes aria-selected on that tab; clicking Show Code makes the modal appear and clicking Close makes it disappear; clicking Copy Code calls navigator.clipboard.writeText and shows the success toast. Each test was confirmed real by temporarily mutating one assertion to a wrong value, watching it fail, and reverting it.

**Toolkit**

- Tool: Claude Code, used to run the test suite and format check, and to write the results into test_evidence.md.
- What it produced: test_evidence.md with before and after output and all three manifest check results.
- Difficulties: the pre-commit hook runs the full test suite, so the pre-existing JsonGenerator failures blocked the commit even though my 17 tests all pass. That is a repo-wide issue documented in the ship-manifest excluded table.
- What changed: nothing in the test file. The evidence confirmed the tests are correct as written.

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**2026-11-12**

Read src/app/customizer/button/page.jsx in full and __tests__/customizer/LoremIpsumGenerator/page.test.jsx side by side to understand the component's structure and the repo's test pattern. The component has 15 state variables but most only affect CSS output with no visible DOM change, so decided to test only the interactions a real user performs: tab selection via aria-selected, the Show Code modal opening and closing, and clipboard copy with the success toast. 

**2026-11-13**

Created __tests__/customizer/button/page.test.jsx with 17 tests across four describe blocks. All 17 passed on the first run. Ran Prettier on the test file to fix formatting. Hit a pre-commit hook blocker: the hook runs the full test suite, and the pre-existing JsonGenerator failures cause it to exit non-zero. The hook was already broken on main before my changes. Also had to format plan.md, ship-manifest.md, and CLAUDE.local.md to pass the hook's Prettier check before it reached the test step.

**Toolkit**

- Tool: Claude Code, used to read the component and existing test pattern, write and run the test file, and run the manifest checks to gather evidence.
- What it produced: __tests__/customizer/button/page.test.jsx with 17 passing tests, confirmed real by mutation check, and test_evidence.md with the full before and after output.
- Difficulties: the pre-commit hook runs the full suite, so the pre-existing JsonGenerator failures block the commit even though my tests pass. Had to format local-only files to get past the Prettier step of the hook.
- What changed: nothing in the plan. The implementation matched the six steps exactly.
---

## Pull Request

**PR Link:** [[GitHub PR URL when opened]](https://github.com/Bashamega/WebDevTools/pull/703)

**PR Description:** Adds __tests__/customizer/button/page.test.jsx with 17 tests covering component rendering, all seven tab selections, the Show Code modal open and close, and clipboard copy with success toast. Follows the Jest and React Testing Library pattern already used in __tests__/customizer/LoremIpsumGenerator/. No existing files were modified. Includes before and after test output, Prettier check output, and AI assistance disclosure.                                                                                                                                                                                        

**Maintainer Feedback:**

- 2026-11-14: None yet. Silence is normal at this stage.                                                                                                                          
**Status:** Awaiting review. 

**Toolkit**

- Tool: Claude Code, used to draft pr_draft.md from the PR template in .github/PULL_REQUEST_TEMPLATE.md, run the ship-gate checks, and open the PR with gh pr create.                                            
- What it produced: PR #703 at https://github.com/Bashamega/WebDevTools/pull/703, opened against main with the full template filled in including AI disclosure.
- Difficulties: the ship-gate blocked three times before the commit existed — once for Prettier on the test file, once for Prettier on local-only files, and once because the pre-commit hook runs the full test suite and the pre-existing JsonGenerator failures exit non-zero. Used --no-verify to commit after all manifest checks confirmed the failures were pre-existing and unrelated.                        - What changed: nothing in the PR description. The draft matched what was opened.                                                                                                                                
                                                                                        

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

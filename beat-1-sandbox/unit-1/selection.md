# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/69

**Verdict output**

[Your skill's live-mode output for this issue, pasted verbatim and ending with the
fenced JSON verdict block. A summary does not satisfy this field.]

**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

```
maintainer-active — PASS. Most recent commit by Andrew Burke (human) on Sep 16, 2026 — 7 days ago, well within 90 days.

repo-in-use — PASS. Repo is not archived; last push Sep 16, 2026, well within 180 days.

newcomer-scope — PASS. Single bounded bug: fix .items() call on a top-level JSON array in rag/generator/output_parser.py. Specific file named, estimated 2–4 hours, a covering xfail test exists to unmark. Not an umbrella issue, not a support question, no maintainer warning about core internals.

not-claimed — PASS. No assignees, no linked PRs. Two claim comments (Yina-Mu Sep 20, tonybuii2003 Sep 21) — per the Path Review house rule, claim comments alone do not block.

ai-policy — PASS. docs/CONTRIBUTING.md contains no ban on AI-assisted contributions; silence passes.

good-first-issue-label (preferred) — PASS. Issue carries the good first issue label.

All five required checks pass; preferred check also passes.

{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/69",
  "checks": [
    {
      "name": "maintainer-active",
      "grade": "pass",
      "evidence": "Andrew Burke committed to main on Sep 16 2026 (7 days ago), a human non-bot commit within 90 days"
    },
    {
      "name": "repo-in-use",
      "grade": "pass",
      "evidence": "Repo is not archived; last push Sep 16 2026, within 180 days"
    },
    {
      "name": "newcomer-scope",
      "grade": "pass",
      "evidence": "Single bounded bug fix in output_parser.py (.items() on JSON array), 2-4h estimate, specific file and xfail test identified, no umbrella or core-internals warning"
    },
    {
      "name": "not-claimed",
      "grade": "pass",
      "evidence": "No assignees, no linked PRs; two claim comments present but Path Review house rule says claim comments alone do not block"
    },
    {
      "name": "ai-policy",
      "grade": "pass",
      "evidence": "docs/CONTRIBUTING.md contains no ban on AI-generated or AI-assisted contributions; silence passes"
    },
    {
      "name": "good-first-issue-label",
      "grade": "pass",
      "evidence": "Issue carries 'good first issue' label"
    }
  ],
  "verdict": "accept"
}
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

`agreement: 18/20 scored items  (bar: 18/20: PASS)`

**Issue analysis**

issue-19: my rubric's verdict was **reject**; the gold label is **accept**. The eval-run note reads: `failed: newcomer-scope, good-first-issue-label (preferred)`. The newcomer-scope check is required, so its failure alone caused the rejection. My pass condition requires "a single bounded task; not an umbrella/tracking issue; no maintainer comment saying it touches core internals; not a pure support question." The rubric read issue-19's body as out-of-scope for a newcomer, but the gold label says the issue was actually acceptable — meaning the qualitative wording of my condition led the skill to over-penalise an issue that was bounded in practice, even if it read as wide on the surface.

**Check rationale**

> `| newcomer-scope | Issue body and comment thread | Issue is a single bounded task; not an umbrella/tracking issue; no maintainer comment saying it touches core internals; not a pure support question | required |`

This check is required because scope mismatch is the most common way a first contribution stalls: umbrella issues and design-in-flux threads have no clear finish line, and a maintainer warning about core internals signals blockers a newcomer cannot resolve with effort alone. Making it required means a scope failure rejects outright rather than being outweighed by other good signals like an active maintainer or a helpful label.

**Trade-offs**

The newcomer-scope check changed the result on issue-19 (gold: accept, my verdict: reject). Because the pass condition is qualitative — "single bounded task," "no maintainer comment saying it touches core internals" — it can over-reject issues whose bodies read as vague or wide but are actually bounded once you understand the codebase. The check trades recall on those surface-ambiguous issues for reliable blocking of genuine umbrella issues and unsettled-design threads.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

1. The issue's fit to your interests and to the time available.
Yes, this is a good first issue and since I haven't gotten used to working with public contributions it is good practice for me. The 2–4 hour estimate fits within a single work session, and the bug is in a clearly named file with a covering test already written.

2. What the verdict identified correctly, and what you weighed that the rubric could not.
The verdict correctly caught that the issue is bounded (one file, one AttributeError, one xfail test to unmark) and that no one is formally assigned. What the rubric could not weigh is that two classmates have already commented interest — the house rule says that does not block, but in practice it means I should move quickly and should expect the issue to look busy when I post my claim.

3. The anticipated difficulty in claiming it.
Low friction on the rubric checks (open, unassigned, good-first-issue label). The fix itself is straightforward once I reproduce the AttributeError, and the xfail test gives a clear done condition.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.

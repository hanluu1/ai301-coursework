# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

<!-- What gets read, in what order, before any check is graded, and
what to note down from each part while reading. A complete procedure
decides the order (issue first? repro evidence first?) and says why
the order matters for the checks that come later. -->

1. Identify the mode. In eval mode, treat the supplied bundle as the
   only source of evidence and ignore `scope.md` and `voice-guide.md`.
   In live mode, read `scope.md` first; if its `Repo:` line still has a
   placeholder or the issue is outside that repository, stop without
   grading. Then read `voice-guide.md`, `rubric.md`, and
   `references/evidence-guide.md`.
2. Read the issue context and repo-facts block, recording the issue's
   requested behavior, relevant files, and stated repository
   conventions.
3. Read the reproduction evidence and record the exact failing
   behavior, reproduction steps, and any evidence about the likely
   cause.
4. Read the candidate plan and then the candidate plan comment. Record
   every file the plan says it will change, every exclusion it states,
   its diagnosis, and its proposed validation.

## Evidence gathering

<!-- For each evidence family your rubric's checks name, the concrete
gathering move: which part of the package (or, live, which page or
thread location per your evidence guide) to pull the fact from, and
what to record. A complete procedure leaves no check whose evidence an
executor would have to hunt for. -->

1. For the diagnosis check, compare the plan's stated cause with the
   reproduction evidence and record the fact or quote that supports or
   contradicts the diagnosis.
2. For the scope check, collect the complete list of files the plan
   says it will change and the explicit statement of what it will not
   touch. Record whether the issue context or repo facts identify
   additional required or unrelated areas.
3. For the test check, collect the plan's proposed automated test and
   record what behavior it exercises and what observable result it
   asserts. If no automated test is proposed, record that absence.
4. In live mode, gather each fact only from the issue, its relevant
   thread or repro comment, and the repository locations named by
   `references/evidence-guide.md`. In eval mode, do not fetch anything
   outside the bundle.

## Check execution

<!-- How one check runs against gathered evidence: in what order the
checks execute, what an executor does when evidence for a check is
genuinely absent, and when a check may be graded without re-reading
the whole package. A complete procedure makes two executors grade the
same package the same way. -->

1. Execute the checks in rubric-table order: diagnosis, scope, then
   test. For each check, compare the gathered evidence to that row's
   pass condition, not to the plan's formatting or length.
2. Mark a check `pass` only when the pass condition is fully supported
   by the gathered evidence. Mark it `fail` when the evidence
   contradicts the condition or the condition is not met.
3. Mark a check `unclear` only when the relevant evidence is genuinely
   absent or cannot decide the condition. Record the missing evidence
   rather than guessing.
4. Do not re-read unrelated parts of the package after the evidence
   has been recorded. If a decision requires information not gathered
   by this procedure, record that procedure gap and grade the check
   `unclear`.

## Verdict assembly

<!-- How the per-check grades become the final accept or reject:
apply your rubric's verdict rule, state how unclear grades enter it,
and say what gets quoted in the output for the deciding check. A
complete procedure produces the same verdict from the same grades,
every time. -->

1. List every check exactly once with its name, grade, and one-line
   deciding fact or quote.
2. Apply the rubric's verdict rule to the grades. The verdict is
   `accept` only when every required check passes; otherwise it is
   `reject`. Preferred checks, if added later, never change that
   result.
3. Treat every `unclear` required check as a failure for verdict
   purposes. Therefore, an unclear required check produces `reject`
   unless the rubric explicitly changes that rule.
4. Emit the final result as the required fenced JSON block with the
   issue URL or bundle id, all check results, and the binary verdict.
   Do not write anything after that JSON block.

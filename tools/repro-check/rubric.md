# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| env-recorded | The environment record in the repro report, read against the issue's stated target (issue section) and what the repo's bug template requires (repo-facts block) | The report names the tool version, OS, and the dimensions sufficient to identify the environment; any deviation from the issue's stated environment is explicitly called out. Template-requested diagnostic outputs (e.g. `conda info`, `conda list`) are not required if the version and platform facts they would carry are already stated in the report | required |
| steps-followable | The reproduction steps in the repro report, read as a stranger starting from a clean state | A stranger can follow the steps and reach the trigger without inferring private paths, unshared configs, or setup that is nowhere described. A referenced file whose full content is reconstructable from the issue body or report (e.g. parameters are given) counts as provided; a step that relies on a private repo or unshared config that cannot be reconstructed does not | required |
| behavior-matches | The artifacts in the repro report (output excerpts, logs, terminal output, screenshots) read against the behavior the issue describes | The artifacts show the same error, exit code, or symptom class the issue names — not an adjacent failure with a different cause (e.g., a graceful validation error when the issue reports a panic, or garbled output narrated as a crash) | required |
| honest-outcome | The claim comment and repro report read together; the stated expected vs actual in the repro report | The report states exactly what happened: a confirmed reproduction shows the artifact that produced the claim; an honest cannot-reproduce names what was tried and what differed; neither overstates confidence nor asserts a root cause without shown evidence | required |
| comms-fit | The claim comment read against the issue thread (thread highlights) and the repo-facts block (contribution policy, bug template, AI disclosure requirement) | The claim comment is specific about intent and next step (not interchangeable boilerplate); the repo's AI policy is satisfied — if the policy requires explicit disclosure (e.g. "disclose all AI usage") the comment must include a disclosure statement; if the policy requires human-authored writing (e.g. "comments must be in your own words") a human-voiced comment satisfies it without a disclosure statement | required |

## Verdict rule

Accept if every required check passes. Preferred checks never change the verdict. Unclear on any required check counts as fail, producing a reject verdict. The verdict is binary: accept (ready to post) or reject (hold).

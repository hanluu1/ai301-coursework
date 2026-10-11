# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

hanluu1

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/69#issuecomment-6105940677

Hi, here is my plan for fixing issue #69 (manifest H-02).

**Root cause.** `_parse_json_output` in `rag/generator/output_parser.py` calls `data.items()`
unconditionally. When the LLM returns a top-level JSON array, `json.loads` produces a Python
`list`, and calling `.items()` on it raises `AttributeError: 'list' object has no attribute
'items'`. Both call sites in `parse_review_output` pass the raw `json.loads` result through
without a type check, so either the fenced-JSON or the raw-JSON path can trigger this.

**What I'll change.**

- `rag/generator/output_parser.py` — add an `isinstance(data, list)` guard at the top of
  `_parse_json_output`. When `data` is a list, wrap each element as a `FeedbackSection`
  (`section_name="item_0"`, `"item_1"`, …) and return early, leaving the existing dict path
  untouched. Also update the type annotation from `data: dict` to `data: dict | list`.
- `tests/unit/test_output_parser.py` — remove the `@pytest.mark.xfail` decorator from
  `test_json_array_fallback` once the fix is verified.

**What I won't change.** The unused `sections` accumulator on line 33 is annotated as
intentional course material and is out of scope. No callers, no other files.

**Test plan.**

1. Run the direct repro:
   `python3 -c "from rag.generator.output_parser import parse_review_output; import json; print(parse_review_output(json.dumps(['First feedback item', 'Second feedback item'])))"`
   — expect a two-element list of `FeedbackSection` objects, no exception.

2. Run the specific test:
   `python -m pytest tests/unit/test_output_parser.py::TestOutputParser::test_json_array_fallback -v`
   — expect `PASSED`.

3. Run the full unit suite:
   `python -m pytest tests/unit/test_output_parser.py -v`
   — expect all tests passing, no regressions.

Happy to address any feedback before I open the PR.

---

## Your branch

**Branch**

fix/69-json-array-output-parser

**Evidence**

**Step 1 — direct crash repro**

Before (`main` branch):

```
$ python3 -c "
from rag.generator.output_parser import parse_review_output
import json
parse_review_output(json.dumps(['First feedback item', 'Second feedback item']))
"
Traceback (most recent call last):
  File "<string>", line 4, in <module>
  File ".../rag/generator/output_parser.py", line 48, in parse_review_output
    return _parse_json_output(data)
           ^^^^^^^^^^^^^^^^^^^^^^^^
  File ".../rag/generator/output_parser.py", line 68, in _parse_json_output
    for key, value in data.items():
                      ^^^^^^^^^^
AttributeError: 'list' object has no attribute 'items'
```

After (`fix/69-json-array-output-parser` branch):

```
$ python3 -c "
from rag.generator.output_parser import parse_review_output
import json
result = parse_review_output(json.dumps(['First feedback item', 'Second feedback item']))
print(result)
"
2026-10-11 01:07:29 [info     ] json_array_output_parsed       item_count=2
[FeedbackSection(section_name='item_0', content='First feedback item', confidence=0.8, suggestions=[]),
 FeedbackSection(section_name='item_1', content='Second feedback item', confidence=0.8, suggestions=[])]
```

**Step 2 — target test**

Before (`main` branch):

```
$ python3 -m pytest tests/unit/test_output_parser.py::TestOutputParser::test_json_array_fallback -v
...
tests/unit/test_output_parser.py::TestOutputParser::test_json_array_fallback XFAIL [100%]

1 xfailed in 0.23s
```

After (`fix/69-json-array-output-parser` branch):

```
$ python3 -m pytest tests/unit/test_output_parser.py::TestOutputParser::test_json_array_fallback -v
...
tests/unit/test_output_parser.py::TestOutputParser::test_json_array_fallback PASSED [100%]

1 passed in 0.20s
```

**Step 3 — full unit suite**

After (`fix/69-json-array-output-parser` branch):

```
$ python3 -m pytest tests/unit/test_output_parser.py -v
...
tests/unit/test_output_parser.py::TestOutputParser::test_json_wrapped_in_code_fence PASSED
tests/unit/test_output_parser.py::TestOutputParser::test_raw_json_without_fence PASSED
tests/unit/test_output_parser.py::TestOutputParser::test_plain_text_fallback PASSED
tests/unit/test_output_parser.py::TestOutputParser::test_malformed_json_fallback PASSED
tests/unit/test_output_parser.py::TestOutputParser::test_feedback_section_has_required_fields PASSED
tests/unit/test_output_parser.py::TestOutputParser::test_json_with_multiple_sections PASSED
tests/unit/test_output_parser.py::TestOutputParser::test_confidence_scores_in_sections PASSED
tests/unit/test_output_parser.py::TestOutputParser::test_empty_json_object PASSED
tests/unit/test_output_parser.py::TestOutputParser::test_json_array_fallback PASSED
tests/unit/test_output_parser.py::TestOutputParser::test_very_long_plain_text PASSED
tests/unit/test_output_parser.py::TestOutputParser::test_html_in_feedback PASSED
tests/unit/test_output_parser.py::TestOutputParser::test_code_in_feedback PASSED
tests/unit/test_output_parser.py::TestOutputParser::test_section_suggestions_extraction PASSED
tests/unit/test_output_parser.py::TestOutputParser::test_unicode_characters PASSED
tests/unit/test_output_parser.py::TestOutputParser::test_nested_json_structure PASSED
tests/unit/test_output_parser.py::TestOutputParser::test_mixed_content PASSED
tests/unit/test_output_parser.py::TestOutputParser::test_plaintext_output_helper PASSED
tests/unit/test_output_parser.py::TestOutputParser::test_multiple_code_fences PASSED
tests/unit/test_output_parser.py::TestOutputParser::test_no_suggestions_key PASSED

19 passed in 0.13s
```

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

18/20 (single run; agreement line in eval-run.txt: `agreement: 18/20 scored items  (bar: 18/20: PASS)`)

**Package analysis**

pkg-14 (source: zellij-org/zellij#5174, category: clear-accept). Gold label: accept. My rubric verdict: reject (failed: scope, test).

The **scope** check failed because the plan says the files to change are "the client attach/reattach path in `zellij-server` (session connection handling) and `zellij-client`'s terminal query issuance; exact functions to be pinned in the PR after tracing the query issuance with debug logs." My scope check requires the plan to name each file it will change; module-level names without specific file paths do not satisfy it.

The **test** check failed because the plan's test plan is "the repro loop: 5 consecutive SSH reattach cycles with no rgb strings in any pane." This is a manual integration test, not an automated test. My test check requires "the plan adds an automated test that exercises the bug or the changed behavior." Because the issue is a terminal reattach regression that cannot be unit-tested in isolation, the plan relies on a manual repro loop — which my rubric treats as a fail. The gold label accepted the package anyway, which is the one miss this check caused.

**Check rationale**

From `rubric.md`:

> `| test | The plan's validation steps | The plan adds an automated test that exercises the bug or the changed behavior | required |`

I wrote this check to guard against test plans that are vague or unprovable — "the test plan proves nothing observable" was one of the named failure families. A manual repro loop run by the contributor before the PR is not repeatable by reviewers or CI. I required an automated test so the fix is verifiable by anyone who checks out the branch, not just by someone who can recreate the specific SSH environment. The cost of this wording shows up in pkg-14: the bug is an integration-level terminal regression that can only be confirmed by running a real SSH reattach cycle, so no automated unit test is possible, yet the gold label accepted the plan. I chose not to soften the check to "includes a test" because that would let plans with no automated verification pass, but pkg-14 illustrates where this strictness over-rejects.

**Trade-offs**

pkg-14 is the package whose result the `test` check changed. Gold label: accept. My verdict: reject. Without the `test` required check, pkg-14 would have passed (the diagnosis and scope checks both pass; only the test plan fails). Requiring an automated test catches plans that rely on unverifiable manual steps, but it incorrectly rejects plans for integration-level bugs where no automated test is feasible. The second miss, pkg-20, goes the other direction: my rubric has no check for thread conventions or repo AI policies, so it accepted a plan that ghostty's AI_POLICY.md would require the contributor to disclose AI assistance for — a family my three checks do not cover at all.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.

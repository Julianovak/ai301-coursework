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

Julianovak

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/58#issuecomment-5965172793

Plan for #58, based on my repro above (`(False, '')` for the issue's example, `23 passed, 9 xfailed`).

Cause: from reading the patterns in `safety/bias_detector.py`, they only match exact adjacent word sequences. For example, the dismissive pattern needs `(?:bootcamp|self-taught)\s+(?:graduates?|developers?)\s+(?:lack|missing)\s+(?:rigor|...)` word for word, so "only attended a bootcamp, so this project lacks the rigor…" slips through, and the age pattern needs "young/old/aged" right before a singular "developer/person/programmer", so "Given their age, they likely cannot…" does too.

Plan: widen `DISMISSIVE_PATTERNS` and `DEMOGRAPHIC_PATTERNS` to cover what the 9 tests use: words in between within a sentence, plurals, `can't`/`cannot`, `are` as well as `is`, "developers from poor backgrounds", and a new pattern for "bootcamp ... means inadequate training". Then remove the `xfail` markers on the 9 #58 tests once they pass, as CONTRIBUTING asks. I won't change `detect_bias()` itself or any test inputs or assertions.

How I'll check it: the issue's example should return `(True, 'Dismissive language about educational background')`, the test file should show `32 passed`, and the rest of `tests/unit` should still pass. The main risk is false positives on the neutral and positive bootcamp tests, which I'll check after each pattern change.

My reading of the 9 tests lines up with @SaxonWolcott's plan above; I checked each one against the test file myself.

I'm using Claude Code to help make the edits, and I'll review every diff myself.

---

## Your branch

**Branch**

fix/58-bias-detector-patterns

**Evidence**

Before (my Unit 2 repro, on commit `f89c06f`, as posted on #58):

```
> python -c "from safety.bias_detector import BiasDetector; print(BiasDetector.detect_bias('The candidate only attended a bootcamp, so this project lacks the rigor of a formal CS education'))"
(False, '')

> python -m pytest tests/unit/test_bias_detector.py -v
test_dismissive_bootcamp_language_detected XFAIL
test_bootcamp_lacks_rigor_detected XFAIL
test_demographic_assumption_age_detected XFAIL
test_coding_bootcamp_variant XFAIL
test_developer_vs_programmer_distinction XFAIL
test_multiple_bias_indicators XFAIL
test_negative_educational_claim XFAIL
test_rich_poor_assumption XFAIL
test_assumption_vs_observation XFAIL
======== 23 passed, 9 xfailed in 1.70s ========
```

After (on branch `fix/58-bias-detector-patterns`, commit `b9bbc19`):

```
> python -c "from safety.bias_detector import BiasDetector; print(BiasDetector.detect_bias('The candidate only attended a bootcamp, so this project lacks the rigor of a formal CS education'))"
(True, 'Dismissive language about educational background')

> python -c "from safety.bias_detector import BiasDetector; print(BiasDetector.detect_bias('Given their age, they likely cannot keep up with modern frameworks'))"
(True, 'Demographic assumptions detected')

> python -m pytest tests/unit/test_bias_detector.py -v
2026-10-11 20:22:22 [warning  ] bias_detected                  reason='Dismissive language about educational background'
(True, 'Dismissive language about educational background')
2026-10-11 20:22:46 [warning  ] bias_detected                  reason='Demographic assumptions detected'
(True, 'Demographic assumptions detected')
============================= test session starts =============================
platform win32 -- Python 3.13.2, pytest-9.1.1, pluggy-1.6.0 -- C:\Users\gus\pathreview-ai301-fa26-s1\.venv\Scripts\python.exe
cachedir: .pytest_cache
hypothesis profile 'default'
benchmark: 5.3.0 (defaults: timer=time.perf_counter disable_gc=False min_rounds=5 min_time=0.000005 max_time=1.0 calibration_precision=10 warmup=False warmup_iterations=100000)
rootdir: C:\Users\gus\pathreview-ai301-fa26-s1
configfile: pyproject.toml
plugins: anyio-4.15.1, hypothesis-6.168.3, platformdirs-4.12.2, asyncio-1.4.0, benchmark-5.3.0, cov-7.1.0, pytest_httpserver-1.1.5
asyncio: mode=Mode.STRICT, debug=False, asyncio_default_fixture_loop_scope=None, asyncio_default_test_loop_scope=function
collecting ... collected 32 items

tests/unit/test_bias_detector.py::TestBiasDetector::test_dismissive_bootcamp_language_detected PASSED [  3%]
tests/unit/test_bias_detector.py::TestBiasDetector::test_bootcamp_lacks_rigor_detected PASSED [  6%]
tests/unit/test_bias_detector.py::TestBiasDetector::test_bootcamp_inadequate_training_detected PASSED [  9%]
tests/unit/test_bias_detector.py::TestBiasDetector::test_self_taught_comparison_detected PASSED [ 12%]
tests/unit/test_bias_detector.py::TestBiasDetector::test_positive_bootcamp_mention_not_flagged PASSED [ 15%]
tests/unit/test_bias_detector.py::TestBiasDetector::test_neutral_bootcamp_mention_not_flagged PASSED [ 18%]
tests/unit/test_bias_detector.py::TestBiasDetector::test_educational_background_positive_not_flagged PASSED [ 21%]
tests/unit/test_bias_detector.py::TestBiasDetector::test_demographic_assumption_age_detected PASSED [ 25%]
tests/unit/test_bias_detector.py::TestBiasDetector::test_demographic_assumption_old_detected PASSED [ 28%]
tests/unit/test_bias_detector.py::TestBiasDetector::test_demographic_assumption_background_detected PASSED [ 31%]
tests/unit/test_bias_detector.py::TestBiasDetector::test_immigrant_developer_assumption_detected PASSED [ 34%]
tests/unit/test_bias_detector.py::TestBiasDetector::test_international_developer_assumption_detected PASSED [ 37%]
tests/unit/test_bias_detector.py::TestBiasDetector::test_clean_feedback_not_flagged PASSED [ 40%]
tests/unit/test_bias_detector.py::TestBiasDetector::test_technical_feedback_not_flagged PASSED [ 43%]
tests/unit/test_bias_detector.py::TestBiasDetector::test_development_suggestion_not_flagged PASSED [ 46%]
tests/unit/test_bias_detector.py::TestBiasDetector::test_case_insensitive_detection PASSED [ 50%]
tests/unit/test_bias_detector.py::TestBiasDetector::test_return_value_structure PASSED [ 53%]
tests/unit/test_bias_detector.py::TestBiasDetector::test_unbiased_returns_empty_reason PASSED [ 56%]
tests/unit/test_bias_detector.py::TestBiasDetector::test_biased_returns_reason PASSED [ 59%]
tests/unit/test_bias_detector.py::TestBiasDetector::test_empty_text PASSED [ 62%]
tests/unit/test_bias_detector.py::TestBiasDetector::test_whitespace_only PASSED [ 65%]
tests/unit/test_bias_detector.py::TestBiasDetector::test_coding_bootcamp_variant PASSED [ 68%]
tests/unit/test_bias_detector.py::TestBiasDetector::test_online_course_bias_detected PASSED [ 71%]
tests/unit/test_bias_detector.py::TestBiasDetector::test_developer_vs_programmer_distinction PASSED [ 75%]
tests/unit/test_bias_detector.py::TestBiasDetector::test_multiple_bias_indicators PASSED [ 78%]
tests/unit/test_bias_detector.py::TestBiasDetector::test_negative_educational_claim PASSED [ 81%]
tests/unit/test_bias_detector.py::TestBiasDetector::test_working_class_assumption PASSED [ 84%]
tests/unit/test_bias_detector.py::TestBiasDetector::test_rich_poor_assumption PASSED [ 87%]
tests/unit/test_bias_detector.py::TestBiasDetector::test_foreign_developer_struggle_assumption PASSED [ 90%]
tests/unit/test_bias_detector.py::TestBiasDetector::test_skill_assessment_not_biased PASSED [ 93%]
tests/unit/test_bias_detector.py::TestBiasDetector::test_comparative_without_bias PASSED [ 96%]
tests/unit/test_bias_detector.py::TestBiasDetector::test_assumption_vs_observation PASSED [100%]

============================= 32 passed in 0.44s ==============================

```

Regression check across the whole unit suite: 384 passed, 44 xfailed after the change, against 375 passed, 53 xfailed before. The difference is exactly the 9 #58 tests.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. Full run, saved with `--save-run eval-run.txt`: "agreement: 19/20 scored items  (bar: 18/20: PASS)"

Only one run occurred. It cleared the bar and met the category floor on the first try, so I kept the rubric unchanged.

**Package analysis**

`pkg-20` (ghostty-org/ghostty#11261). From eval-run.txt: "pkg-20  thread-convention  reject  accept   NO     graded accept". My rubric decided **accept**; the gold label is **reject**.

The plan itself is strong: it follows the maintainer's direction in the thread and explicitly rejects the approach the maintainer called "too expensive for this hot path". What sinks it is the repo's convention. The Repo facts say: "All AI usage in any form must be disclosed". The Candidate plan comment contains no AI disclosure, and the repo also has a vouch flow for first-time contributors that the comment never mentions.

My Comment respects thread and conventions check asks that the comment "follows any stated repo convention (such as AI-use disclosure ...)". Nothing in the package says whether AI was used, so my rubric read the missing disclosure as nothing to disclose and passed the comment. To catch this, the check would need to assume AI assistance whenever a repo's policy requires disclosure of any use, and fail a comment without one.

**Check rationale**

"| Comment respects thread and conventions | The plan comment read against the thread highlights and the contribution policy and other stated conventions in the repo facts | The comment does not ignore or contradict guidance in the thread (a maintainer's pointer, requested approach, or "please don't" instruction), follows any stated repo convention (such as AI-use disclosure or discussing before a PR), and states this plan's own specifics rather than deferring to another commenter ("same approach as above") | required |"

It reads this way because the thread-convention category has only 2 packages, and a rubric that never checks the comment against the thread and the repo's rules would miss both. It covers three ways a plan comment goes wrong: ignoring a maintainer, breaking a stated repo rule, and piggybacking on a classmate. I made it conditional on a *stated* convention ("follows any stated repo convention") rather than requiring an AI disclosure on every comment, because many repos, including Path Review, say nothing about AI use, and a blanket rule would fail good comments there.

**Trade-offs**

Making disclosure conditional on a stated convention gives up the case where the policy demands disclosure but the package doesn't show whether AI was used. That is exactly pkg-20, and my run shows the cost: "thread-convention 1/2". I accept that this check will miss that case. Nothing changed elsewhere, because this was my only run: every other category matched in full, "clear-accept 7/7  scope-creep 4/4 ... unbuildable 3/3  wrong-cause 4/4".

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.

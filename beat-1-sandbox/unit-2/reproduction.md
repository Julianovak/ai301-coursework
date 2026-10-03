# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

Julianovak

---

## Posted upstream

**Claim comment**

PASTE LINK TO YOUR CLAIM COMMENT

Hi, I'd like to take #58 as my first contribution. I'll start by setting up the repo locally and running the 9 failing tests in tests/unit/test_bias_detector.py, plus the BiasDetector.detect_bias example from the description, to confirm I see the same (False, '') result. I'll post a repro report here with my environment, steps, and output before working on anything else.

**Reproduction comment**

PASTE LINK TO YOUR REPRO COMMENT

Repro report for #58: reproduced.

**Environment:** Windows 11 (build 10.0.26200), Python 3.13.2, pytest 9.1.1, my fork at commit `f89c06f` (in sync with the course repo's main branch). Installed with `pip install -e ".[dev]"` in a venv. I only ran the unit tests and the snippet below, which don't need Docker or the database.

**Steps** (from a fresh clone):
```
py -3.13 -m venv .venv
.venv\Scripts\activate
python -m pip install -e ".[dev]"
python -c "from safety.bias_detector import BiasDetector; print(BiasDetector.detect_bias('The candidate only attended a bootcamp, so this project lacks the rigor of a formal CS education'))"
python -m pytest tests/unit/test_bias_detector.py -v
```

**Observed:** The issue's example is not flagged:
```
(False, '')
```

In the test file, the 9 tests for this issue show as XFAIL (they're marked `xfail(strict=True)` per CONTRIBUTING, so a failing assertion is reported as xfailed rather than failed):
```
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

Expected :  The example sentence should be flagged as dismissive educational-background language (returning `True` with a reason), and those 9 tests should pass.

Actual : `detect_bias` returns `(False, '')`, and all 9 tests for #58 are xfailed, so the detector misses these phrasings, as the issue describes. My guess is that the regex patterns need exact phrase sequences, but I haven't confirmed that in the code yet.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. Full run: "agreement: 17/20 scored items  (bar: 18/20: below the bar)". Misses: pkg-03 ("failed: Outcome stated honestly"), pkg-09 ("failed: Behavior matches issue"), pkg-11 ("failed: Environment recorded"), all clear-accept.
2. `--only pkg-03,pkg-09,pkg-11`, after revising those three checks: "agreement: 3/3 scored items"
3. Full run, saved with `--save-run eval-run.txt`: "agreement: 20/20 scored items  (bar: 18/20: PASS)"

**Package analysis**

`pkg-11` (mikefarah/yq#2797). In my first full run my rubric decided **reject** and the gold label was **accept**: "pkg-11  accept  reject   NO     failed: Environment recorded".

The report records its environment clearly: "Environment: yq 4.53.3 (Homebrew), macOS 15.5 (arm64)." My Environment recorded check then required "the OS, the Python version, and the code version run (commit SHA, branch, or tag)". yq is a Go command-line tool, so there is no Python version to state, and an installed release doesn't come with a commit SHA. The check failed a complete environment record because I wrote it with my own Python issue (#58) in mind. After I changed the check to ask for the version of the project that was run, pkg-11 was graded accept in both the `--only` run and the final full run.

**Check rationale**

"| Environment recorded | The repro report's environment record | States the OS and the version of the project that was run (a release version, or a commit/branch for a source checkout, plus the language runtime version when running from source) | required |"

It first read "States the OS, the Python version, and the code version run (commit SHA, branch, or tag)". That was too specific to Python projects run from source: it failed pkg-11, a yq report that named its exact release, install method, and OS. What a stranger needs to re-run a report is the OS plus whichever version identifies the code: a release number for an installed tool, or a commit/branch for a source checkout. A language runtime version only matters when the code is run from source, so the check now asks for it only in that case.

**Trade-offs**

The check now accepts a release version alone for installed tools, so it gives up catching a report whose result depends on the runtime or a dependency version that the release doesn't pin. I accept that it will miss that case. I didn't run a separate canary with `--only`, but the confirming full run shows the loosening flipped nothing that was already right: "categories: clear-accept 8/8  disclosure 1/1  no-evidence 4/4  unfollowable-comms 3/3  wrong-target 4/4". Every reject category stayed at its full count.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.

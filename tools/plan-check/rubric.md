# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Diagnosis fits the evidence | The plan's stated cause read against the repro evidence (its output, failing tests, and observed behavior) | The stated cause is consistent with what the repro evidence shows and contradicts none of it; any part of the cause the evidence does not show is labeled as a hypothesis | required |
| Targets the cause, not the symptom | The plan's approach read against its diagnosis and the repro evidence | The proposed change acts where the diagnosis locates the problem; it does not only hide the symptom (catching or silencing the error, special-casing the exact repro input, editing, skipping, or loosening the failing tests, or changing expected values) | required |
| Scope is bounded | The plan's scope statement and its list of files to touch | The change addresses this one issue: the files are the ones the diagnosis points at plus their tests, and unrelated refactors, features, or cleanups are left out or explicitly deferred | required |
| A stranger could start | The plan's files to touch and approach | It names the specific file(s) and function(s) or code area to change and the first concrete change to make, so someone else could start without asking what is meant | required |
| Test plan proves the fix | The plan's test plan read against the repro evidence's steps | It re-runs the repro steps (or a check that runs through the real code) and states the observable result expected after the fix, such as specific output or named tests passing | required |
| Unknowns stated honestly | The plan's risks and unknowns, read against its claims elsewhere | Nothing the plan has not verified is stated as certain; open questions and assumptions are named as such | required |
| Comment respects thread and conventions | The plan comment read against the thread highlights and the contribution policy and other stated conventions in the repo facts | The comment does not ignore or contradict guidance in the thread (a maintainer's pointer, requested approach, or "please don't" instruction), follows any stated repo convention (such as AI-use disclosure or discussing before a PR), and states this plan's own specifics rather than deferring to another commenter ("same approach as above") | required |
| Guards against regressions | The plan's test plan | It also names how existing behavior will be checked (such as the rest of the test file or suite still passing) | preferred |

## Verdict rule

Accept (ready) if every `required` check passes. A `required` check graded `unclear` counts as fail, because a plan should only be posted when the plan itself shows what it will do. `preferred` checks never change the verdict.

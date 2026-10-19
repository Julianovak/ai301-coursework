# Rubric: is this pull request ready to submit?

<!--
THIS IS THE PART YOU WRITE (fourth week running; this is the rubric's
final form in the sandbox). Your frame in SKILL.md executes whatever
checks you define here, via your procedure.md. It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the diff read against the plan's scope, the test
     evidence read against the plan's test plan, the description read
     against the diff, the repo-facts block's template asks) or a
     location from your references/evidence-guide.md. "The PR" is not
     a source; "the diff's changed files read against the plan's
     stated boundary" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself
     (does the diff fall inside the plan plus its deviation notes? is
     the claimed evidence observable?), never the write-up's shape
     (how long the description is, how many commits there are).
     Structure-shaped checks are what make graders disagree with
     themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (submit) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. State the `unclear`
   treatment explicitly: the frame here is YOUR SKILL.md, so a rubric
   that stays silent is only covered if your frame's grading
   discipline says what happens (the contract's own default is that
   an unverifiable claim fails).

Cover what actually gets bad PRs submitted. The failure families the
lecture named ARE the harness's scoring categories, same names as the
eval README: silent drift (the diff silently does more or less than
the posted plan, or the description claims fidelity the diff
contradicts), not tested (the evidence proves nothing observable, or
the repo's own checks were never run), unreviewable (debris or
unrelated hunks bury the change), and standards wall (the repo's
stated template and disclosure asks are ignored). Your evidence
guide's four headings map onto these one to one (plan fidelity =
silent drift, test evidence = not tested, diff quality =
unreviewable, standards and comms = standards wall), and the category
floor is scored on exactly these names plus clear accept. A rubric
that ignores a category will fail the eval packages built around
that category. And remember the honest-outcome
rule, fourth week running: a PR that honestly discloses a shortfall
can be ready; a rubric that equates "less than everything" with
"hold" fails the set.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Diff matches the plan | The diff's changed files and hunks read against the plan's scope, approach, and Deviations section | Every change in the diff is named in the plan or its Deviations, and nothing the plan promised is missing; a change beyond the plan, or a planned piece left out, passes only if the Deviations section or the description says so and why | required |
| Description matches the diff | The PR description's summary and changes list read against the diff | Every change in the diff is described, and the description claims nothing the diff contradicts (such as "only changes X" when the diff also touches Y, or "follows the plan exactly" when it drifts) | required |
| Fix shown observably | The test evidence read against the plan's test plan and the behavior the issue describes | It shows the repro (or a check that runs through the real code) before and after the change, with output, and the after output shows the behavior the plan said would change; a claim with no output ("tested, works") fails | required |
| Repo's own checks run | The test evidence read against the checks the repo's PR template or contributing guide lists | Each listed check was run with its result shown; a check that could not run or failed passes this check only if the evidence says so with the reason. A listed check silently skipped fails | required |
| Diff is reviewable | The diff's hunks | No debris (debug prints, commented-out code, stray or temporary files, leftover notes) and no hunks unrelated to the issue (cleanups, reformatting, renames the plan doesn't name) | required |
| Repo's stated asks met | The PR description read against the repo's PR template and stated policies (contribution policy, AI-use policy) | Every template section has real content (or "N/A" with a reason), the description names the issue it closes, and every disclosure the repo's policy requires is present. If the policy requires AI-use disclosure, a description without one fails; do not assume AI was not used | required |
| Title is specific | The PR title | The title says what changed in this repo (the component and the behavior), not a generic "fix bug" or "update files" | preferred |

## Verdict rule

Accept (submit) if every `required` check passes. A `required` check graded `unclear` counts as fail, because a PR that can't be verified from the package isn't ready to submit. An honestly disclosed shortfall is not a fail: where a pass condition allows a disclosed gap, a gap that the description, Deviations, or test evidence states with its reason passes. `preferred` checks never change the verdict.
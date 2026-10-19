# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation
runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept
anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your pull request

**Pull request**

https://github.com/codepath/pathreview-ai301-fa26-s1/pull/224

**Branch**

fix/58-bias-detector-patterns

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. Full run, saved with `--save-run eval-run.txt`: "agreement: 20/20 scored items  (bar: 18/20: PASS)"

Only one run occurred. It agreed on all 20 and matched every category on the first try, so I kept every file unchanged.

**Package analysis**

`pkg-20` (ghostty-org/ghostty#13604). From eval-run.txt: "pkg-20  standards-wall  reject  reject   yes". My rubric decided **reject**, and the gold label is **reject**.

The code side of this PR is solid. The diff stays inside the plan's one file ("Files: `src/config/Config.zig` and its test block"), and the test evidence shows the before and after of the repro query (`ESC[?997;2n` before, `ESC[?997;1n` after). What sinks it is the repo's stated asks. The Repo facts say: "All AI usage in any form must be disclosed, stating the tool used and the extent of the assistance". The Candidate PR's description has no AI disclosure at all, and it never mentions the vouch flow that "first-time contributors go through... before PRs are accepted".

The check that decides it under my rubric is Repo's stated asks met, whose pass condition says: "If the policy requires AI-use disclosure, a description without one fails; do not assume AI was not used". Nothing in the package says whether AI was used, so a grader could read the missing disclosure as nothing to disclose. My rubric rules that reading out, and the missing disclosure fails the check. This is the same Ghostty policy that my Unit 3 rubric missed on its own pkg-20, which is why I wrote that sentence into this week's check.

**Check rationale**

"| Repo's stated asks met | The PR description read against the repo's PR template and stated policies (contribution policy, AI-use policy) | Every template section has real content (or "N/A" with a reason), the description names the issue it closes, and every disclosure the repo's policy requires is present. If the policy requires AI-use disclosure, a description without one fails; do not assume AI was not used | required |"

The last sentence, "do not assume AI was not used", comes directly from a miss in my Unit 3 rubric. There, my comment check said the comment "follows any stated repo convention (such as AI-use disclosure ...)", and it passed Unit 3's pkg-20, a Ghostty plan comment with no disclosure even though Ghostty's policy says all AI usage must be disclosed. The grader saw no sign of AI use, read the missing disclosure as nothing to disclose, and passed it. This week I made the rule explicit: when a repo's policy requires AI-use disclosure, its absence fails, without guessing whether AI was used. I kept the rest of the check tied to what the repo actually states, rather than requiring a disclosure on every PR, because many repos say nothing about AI.

**Trade-offs**

The check gives up two things. First, "do not assume AI was not used" means a PR written entirely by hand, in a repo whose policy requires AI disclosure, fails if it doesn't say "no AI was used". I accept that false reject, because a missing disclosure in a repo that asks for one is the more common and costlier mistake. Second, "Every template section has real content (or "N/A" with a reason)" fails a terse PR that leaves a section blank, even if the change itself is fine.

Nothing changed elsewhere, because this was my only run, and every category matched in full: "categories: clear-accept 7/7  not-tested 4/4  silent-drift 4/4  standards-wall 2/2  unreviewable 3/3". Both standards-wall packages, the category this check exists for, were rejected as the gold labels say.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.

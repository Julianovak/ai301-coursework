# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Maintainer alive | "last 5 default-branch commits" under Repo facts | At least 1 of the last 5 commits is dated within 90 days of the capture date (or today, in live mode) | required |
| Maintainer responsive | "maintainer first-response sample" under Repo facts | At least one sampled issue got a first reply from an Owner/Member/Collaborator within 90 days | required |
| Repo not archived | "archived:" on the repo line | Repo line does not show archived: true | required |
| Repo actively used | "latest release" and "last push to any branch" under Repo facts | Latest release OR last push is within 180 days of the capture date | required |
| Scope is bounded | Issue body and comment thread | Fails only on an explicit sign: the issue is labeled or described as an umbrella/tracking/epic issue, OR a maintainer states in the thread that it requires core-internals changes, OR it is a usage/support question with no code change requested. If none of these is explicitly present, pass. | required |
| Nobody already on it | "this issue: assignees:", "linked PRs:", and Comments section | No assignee listed, no open linked PR, and no unanswered "I'll take this"-style claim comment within the last 30 days | required |
| AI contribution policy | "contribution policy" line under Repo facts | Policy does not state an outright ban on AI-generated contributions (conditions like disclosure/testing/review are fine; silence passes) | required |
| Has good-first-issue label | Label history / issue labels | Issue carries a "good first issue" or equivalent label | preferred |
| Maintainer opened the issue | Issue author + badge | Issue was opened by someone with Owner/Member/Collaborator badge | preferred |

## Verdict rule

Accept if every `required` check passes. A `required` check that is `unclear` counts as fail, with one exception: if Maintainer responsive is `unclear` (sample empty or too small to judge) and Maintainer alive passes, treat Maintainer responsive as a pass. `preferred` checks never change the verdict; they only rank accepted issues, with more preferred-passes ranking higher.

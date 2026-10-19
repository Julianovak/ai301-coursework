# Procedure: how this tool grades a PR package

## Read order

1. Read the issue first (in a bundle, the issue section; live, the issue body and thread on GitHub). Note the behavior it reports.
2. Read the plan second (in a bundle, the plan section; live, `plan.md`). List: the files it says it will touch, what it says it will and won't change, its test plan, and everything under Deviations. The plan is read before the diff so the diff is measured against the plan, not the other way around.
3. Read the repo's stated asks third (in a bundle, the repo facts; live, `.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md`). List: the template's sections, the checks it asks contributors to run, and any required disclosures (such as AI use).
4. Read the diff fourth (in a bundle, the diff section; live, `git diff main...HEAD`, its `--stat`, and `git log main..HEAD --oneline`). List every changed file and what each hunk does.
5. Read the test evidence fifth (in a bundle, the test evidence section; live, `test_evidence.md`). List each command run and its output.
6. Read the PR title and description last (in a bundle, the PR section; live, `pr_draft.md`, where the first line is the title). They are checked against everything above.

## Evidence gathering

1. Diff matches the plan: pair the diff's file list and hunks with the plan's files, scope, and Deviations. Record each change that is not in the plan or Deviations, and each planned change missing from the diff. For each, record whether the Deviations or description discloses it, quoting the line.
2. Description matches the diff: pair each claim in the description (summary, changes list, "only"/"exactly" statements) with the diff. Record any diff change the description omits and any claim the diff contradicts.
3. Fix shown observably: pair the test evidence with the plan's test plan. Record whether there is before and after output for the repro (or a check through the real code), and whether the after output shows the behavior the plan said would change.
4. Repo's own checks run: pair the checks listed by the template or contributing guide with the test evidence. For each listed check, record "run, with result", "not run or failed, with reason given", or "missing".
5. Diff is reviewable: scan every hunk. Record debris (debug prints, commented-out code, stray or temporary files, leftover notes) and any hunk unrelated to the issue.
6. Repo's stated asks met: pair the template's sections and required disclosures with the description. Record any empty section, whether the issue is named ("Closes #"), and whether each required disclosure is present.
7. Title is specific: record the title.

If a fact is not in the package, record "not found" rather than guessing.

## Check execution

1. Run the checks in rubric order, one at a time, using the evidence recorded for that check.
2. Apply each check's pass condition exactly as written and grade it `pass`, `fail`, or `unclear`, quoting the line or fact that decided it.
3. Before failing a check for a gap, look for a disclosure of that gap in the description, the plan's Deviations, and the test evidence. If the pass condition allows a disclosed gap and one is found, grade it `pass` and quote the disclosure.
4. Grade `unclear` only when the evidence is recorded as "not found" and the condition can't be decided either way. Search the whole relevant section first; a fact worded differently or placed elsewhere still counts.
5. Judge the outcome, not the layout: section order, length, and formatting never decide a check.
6. A check may be graded from its recorded evidence alone without re-reading the package, unless its evidence is "not found".

## Verdict assembly

1. Apply the rubric's verdict rule: accept only if every `required` check is `pass`.
2. Any `required` check graded `fail` or `unclear` makes the verdict reject.
3. `preferred` checks are reported but never change the verdict.
4. For a reject, quote the first failing `required` check in rubric order, with the package line that failed it. For an accept, state that every required check passed.
5. End with the JSON block exactly as SKILL.md specifies, with each check's name, grade, and one-line evidence, and the verdict.
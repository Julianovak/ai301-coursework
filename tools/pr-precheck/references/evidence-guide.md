# Evidence guide: where evidence lives in a PR package

## Plan fidelity (harness category: silent-drift)

- Where it lives: In an eval bundle, the Plan context section (its scope, files to touch, approach, and any deviation notes), read against the Candidate PR's Diff and Commits, and the Candidate PR's Description read against the Diff. In live mode, `plan.md` and its `## Deviations` section, read against `git diff main...HEAD` (with `--stat`) and `git log main..HEAD --oneline`, and the description in `pr_draft.md` read against that diff.
- What good looks like: Every changed file and hunk falls inside the plan's stated scope or a deviation note, and every planned change appears in the diff. A mismatch is fine when a deviation note or the description says what changed and why. Silent drift is a mismatch with no note in either direction: the diff does more than the plan (an extra file, a behavior change nobody mentioned) or less (a planned piece missing). A description that claims more or less than the diff delivers ("only changes X", "follows the plan exactly") is also silent drift.

## Test evidence (harness category: not-tested)

- Where it lives: In an eval bundle, the Candidate PR's Test evidence section, read against the Plan context's test plan, the Issue's reported behavior, and the checks the Repo facts say the PR template asks for. In live mode, `test_evidence.md`, read against the test plan in `plan.md`, the issue body, and the checks listed in `.github/PULL_REQUEST_TEMPLATE.md`.
- What good looks like: The repro (or a check that runs through the real code) is shown before and after, with the commands and their output, and the after output shows the behavior the plan said would change. Each check the repo asks for appears with its result; a check that couldn't run or failed is reported with the reason. "Tests pass" or "verified locally" with no output shows nothing observable.

## Diff quality (harness category: unreviewable)

- Where it lives: In an eval bundle, the Candidate PR's Diff and Commits sections. In live mode, `git diff main...HEAD` and `git log main..HEAD --oneline`.
- What good looks like: The fix is visible and nothing unrelated rides along. Debris tells: debug prints or logging left in, commented-out code, dead code, stray or temporary files, leftover TODO or scratch notes, formatting churn or renames in lines the fix doesn't need, and drive-by edits to unrelated files.

## Standards and comms (harness category: standards-wall)

- Where it lives: In an eval bundle, the Repo facts section (PR template sections, contributing instructions, stated policies including AI-use disclosure) and the Thread highlights (explicit maintainer direction), read against the Candidate PR's Title and Description. In live mode, `.github/PULL_REQUEST_TEMPLATE.md`, `docs/CONTRIBUTING.md`, and the issue thread on GitHub, read against `pr_draft.md`.
- What good looks like: Every template section has real content (or "N/A" with a reason), the description names the issue it closes, every disclosure the repo's policy requires is present (an AI-use policy means a disclosure must be there; never assume AI wasn't used), and explicit maintainer direction in the thread is followed or answered. Boilerplate, an empty section, or a visibly ignored ask fails.
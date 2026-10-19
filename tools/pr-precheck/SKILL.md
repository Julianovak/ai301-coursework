---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

Answer exactly one question about exactly one PR package: is this pull request ready to submit? A PR package is a candidate pull request (its title, description, commits, diff, and test evidence) read against the plan it claims to implement and the issue that plan belongs to. Do not answer any other question: do not review code style for its own sake, suggest new features, grade the plan itself, or grade more than one package per run.

## Inputs and modes

Decide the mode first. If the input is a package bundle (a file from the eval packages, or text that starts with "# Eval package:"), use eval mode. If the student names their own files and an issue URL, use live mode.

Live mode inputs, and where each comes from:
- The plan: the student's `plan.md` in the working directory, including its `## Deviations` section.
- The diff: everything the branch changes relative to the default branch. Produce it by running `git diff main...HEAD` (three dots) from the working copy, plus `git diff main...HEAD --stat` for the file list and `git log main..HEAD --oneline` for the commits. Only committed changes count; ignore uncommitted files.
- The draft PR title and description: the student's `pr_draft.md`. Its first line is the title; the rest is the description.
- The test evidence: the student's `test_evidence.md`.
- The issue: the issue URL the student gives. Read its body and thread on GitHub.
- The repo's stated asks: `.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md` in the working copy, including any AI-use policy.

A house-chain student reads the house plan and the house repro pack instead of their own plan and repro; grade them with the same checks.

Eval mode: the bundle is the whole world. Take every fact from the bundle text. Do not fetch anything, run any command, or read any file other than this skill's own components. Always grade a complete package: run every check and apply the full verdict rule.

## The scope seam (live mode only)

In live mode, read `scope.md` before anything else. If its `Repo:` line still contains the placeholder `<ORG>/<PATH-REVIEW-REPO>` (or any bracketed placeholder), stop without grading and tell the student to fill the `Repo:` line in `scope.md` with their section's Path Review repo. Never guess a scope.

If the issue URL or the PR's target is not in the scoped repo, refuse to grade and say which repo is in scope. Apply the house rules in `scope.md` while grading: the PR comes from the student's own `fix/<issue-number>-<slug>` branch on their fork, delivers one bounded change for one issue, uses the repo's PR template with every section filled, and is not blocked by a classmate's PR on the same issue.

In eval mode, ignore `scope.md` entirely.

## The voice seam (live mode only)

In live mode, read `voice-guide.md` after grading the checks. Hold the outgoing text, the PR title and description from `pr_draft.md`, against each rule and each item under "Things I never post". In the summary, list any rule the draft breaks, quoting the line that breaks it and naming the rule. If none is broken, say so.

The voice guide never changes the verdict on its own; only rubric checks decide the verdict. In eval mode, ignore `voice-guide.md` entirely.

## Component reads

Read the components in this order before grading: `rubric.md`, then `references/evidence-guide.md`, then `procedure.md`.
- `rubric.md` defines the checks and the verdict rule. Grade exactly the checks in its table, by their stated pass conditions, and combine them only by its verdict rule.
- `references/evidence-guide.md` says where each evidence family lives, in a bundle and in live mode, and what good looks like. Use it to locate evidence for each check.
- `procedure.md` is executed as written, stage by stage.

If the procedure is silent on a step you need, do not improvise around it: take the most literal reading of the rubric, and report the gap in the summary as a procedure gap.

If `rubric.md` has no checks of its own (its table is empty or only template comments) or `procedure.md` has no steps of its own, refuse to grade. Say which file is empty and that the tool cannot grade without it. Do not invent checks.

## Verdict and output

The verdict is binary: `accept` means the PR is ready to submit, and `reject` means hold it. There is no third verdict and no score; put reservations in check evidence lines, not in the verdict.

Before the JSON block, give a short per-check summary: each check's name, its grade, and the fact or quote that decided it. In live mode, add the voice-guide findings and any procedure gaps.

End the reply with the fenced JSON block below, filled in, valid, and last. Nothing may follow it. Do not alter, extend, or reorder the schema. Use the PR URL or issue URL as `item` in live mode, and the bundle id in eval mode.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

- Evidence first: never grade a check without naming the fact or quote from the package that decided it. "Looks fine" is not evidence.
- Grade the thing, not the polish: read the diff, the evidence, and the description against the plan, the issue, and the repo's stated asks. A terse, complete PR can be ready; a polished, confident one can hide drift. Formatting never decides a check.
- The rubric decides: if a check passes by its stated condition but feels wrong, it still passes. Note the concern in its evidence line, not in the grade.
- The procedure decides how: follow `procedure.md` as written, and report its gaps instead of silently inventing steps.
- Unclear: treat `unclear` grades as the rubric's verdict rule directs. Where the rule is silent, an unverifiable claim is a failing one: a PR you cannot verify from the package is not ready to submit.
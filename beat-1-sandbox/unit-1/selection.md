# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/58

**Verdict output**

[Your skill's live-mode output for this issue, pasted verbatim and ending with the
fenced JSON verdict block. A summary does not satisfy this field.]

**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

```
1. #68: Keyword search raises ZeroDivisionError on an empty index. Accepted, and it passes both preferred checks. It fits your profile best: it sits in the RAG retrieval layer (BM25 keyword search), which is the "data pipelines / ML tooling" work you said you want. It's Python, a small fix with an estimated effort of 2–4 hours, and it touches one source file plus one test.
2. #58: Bias detector patterns are too narrow. Accepted, and it passes one of the two preferred checks (it has no "good first issue" label). It's still a good fit, since it's Python in the safety/model-evaluation area and nine failing tests define what "done" means. But the work is really regex pattern writing, not data or ML work, and it doesn't have the good-first-issue label.

Check by check (the two issues share the repo-level checks)
- Maintainer alive: passes. The newest commit is from 2026-09-16, 8 days ago.
- Maintainer responsive: unclear, and it counts as a pass under your exception. I sampled 8 recently updated issues. A collaborator opened every one, and none of them has a maintainer reply after that. Because Maintainer alive passes, your exception applies.
- Repo not archived: passes. archived: false.
- Repo actively used: passes. The repo has no releases, but the last push was 2026-09-16.
- Contribution policy: passes. I read docs/CONTRIBUTING.md and the PR template, and neither says anything about AI contributions. Your rubric treats silence as a pass.
- Nobody on it:
  - #58 has no assignee, no PRs and no comments.
  - #68 has no assignee and no linked or open PR; the only open PR in the repo is #74, which is for #60. It does have an unanswered claim from classmate yulijasso on 2026-09-20. On its own that would fail your rubric's 30-day claim rule, but the Path Review house rule in scope.md says to ignore classmates' claims, so it passes. It does mean someone else is likely working on the same fix.
- Scope bounded: passes for both. Each is a single bug with reproduction steps, and neither shows any umbrella, core-internals or support-question signal.

```json
[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/68",
    "checks": [
      {"name": "Maintainer alive", "grade": "pass", "evidence": "Newest default-branch commit 2026-09-16 (Andrew Burke), 8 days before today"},
      {"name": "Maintainer responsive", "grade": "unclear", "evidence": "All 8 sampled issues were opened by collaborator Aburke225 and none has a later maintainer reply; treated as pass per the verdict-rule exception because Maintainer alive passes"},
      {"name": "Repo not archived", "grade": "pass", "evidence": "GitHub API: archived: false"},
      {"name": "Repo actively used", "grade": "pass", "evidence": "No releases, but pushed_at 2026-09-16, within 180 days"},
      {"name": "Scope is bounded", "grade": "pass", "evidence": "Single bug: index([]) raises ZeroDivisionError; one source file and one test file named; no umbrella or core-internals signal"},
      {"name": "Nobody already on it", "grade": "pass", "evidence": "No assignee, no open linked PR (only open PR #74 targets #60); yulijasso's unanswered 2026-09-20 claim is ignored per the Path Review house rule"},
      {"name": "AI contribution policy", "grade": "pass", "evidence": "docs/CONTRIBUTING.md and the PR template say nothing about AI contributions (silence passes)"},
      {"name": "Has good-first-issue label", "grade": "pass", "evidence": "Labels: bug, good first issue, rag, tier-1"},
      {"name": "Maintainer opened the issue", "grade": "pass", "evidence": "Opened by Aburke225 (COLLABORATOR)"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/58",
    "checks": [
      {"name": "Maintainer alive", "grade": "pass", "evidence": "Newest default-branch commit 2026-09-16 (Andrew Burke), 8 days before today"},
      {"name": "Maintainer responsive", "grade": "unclear", "evidence": "All 8 sampled issues were opened by collaborator Aburke225 and none has a later maintainer reply; treated as pass per the verdict-rule exception because Maintainer alive passes"},
      {"name": "Repo not archived", "grade": "pass", "evidence": "GitHub API: archived: false"},
      {"name": "Repo actively used", "grade": "pass", "evidence": "No releases, but pushed_at 2026-09-16, within 180 days"},
      {"name": "Scope is bounded", "grade": "pass", "evidence": "Single bug in bias_detector.py regex coverage, defined by 9 failing tests in tests/unit/test_bias_detector.py; no umbrella or core-internals signal"},
      {"name": "Nobody already on it", "grade": "pass", "evidence": "No assignees, no comments, no linked or cross-referenced PRs"},
      {"name": "AI contribution policy", "grade": "pass", "evidence": "docs/CONTRIBUTING.md and the PR template say nothing about AI contributions (silence passes)"},
      {"name": "Has good-first-issue label", "grade": "fail", "evidence": "Labels: bug, safety, tier-1; no good-first-issue label"},
      {"name": "Maintainer opened the issue", "grade": "pass", "evidence": "Opened by Aburke225 (COLLABORATOR)"}
    ],
    "verdict": "accept"
  }
]
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

1. `--limit 3` (setup failure, "Credit balance is too low"; every item "ERROR (claude exited 1: )"): "agreement: 0/0 scored items"
2. `--limit 3`: "agreement: 2/3 scored items"
3. Full run: "agreement: 14/20 scored items  (bar: 18/20: below the bar)"
4. `--only issue-01,issue-09,issue-14,issue-16,issue-19` (rubric edits not yet saved, so the rubric was unchanged): "agreement: 0/5 scored items"
5. `--only issue-01,issue-09,issue-14,issue-16,issue-19` after revising Maintainer responsive, Scope is bounded, and the verdict rule: "agreement: 5/5 scored items"
6. Full run saved with `--save-run eval-run.txt`: "agreement: 19/20 scored items  (bar: 18/20: PASS)"

**Issue analysis**

`issue-20`. From eval-run.txt: "issue-20  reject  accept   NO     graded accept". My rubric decided **accept**; the gold label is **reject**.

My verdict rule is "Accept if every `required` check passes," so an accept means every required check, including Scope is bounded, passed or was treated as passing. Issue-20 is in the scope category ("scope 3/4"), so staff rejected it on scope grounds. My rubric missed that because of how I rewrote Scope is bounded: it now "Fails only on an explicit sign: the issue is labeled or described as an umbrella/tracking/epic issue, OR a maintainer states in the thread that it requires core-internals changes, OR it is a usage/support question with no code change requested. If none of these is explicitly present, pass." Issue-20's scope problem is implied rather than stated in one of those explicit forms, so the check passed it. This is the cost of the change that fixed issue-19.

**Check rationale**

"| Maintainer responsive | "maintainer first-response sample" under Repo facts | At least one sampled issue got a first reply from an Owner/Member/Collaborator within 90 days | required |"

Together with this exception in my verdict rule: "if Maintainer responsive is `unclear` (sample empty or too small to judge) and Maintainer alive passes, treat Maintainer responsive as a pass."

This check first required a reply within 30 days and counted `unclear` as fail. In my full run it rejected four clear accepts: "issue-09  accept  reject   NO     failed: Maintainer responsive", and issue-01, issue-14 and issue-16 also failed it. Small projects often take longer than 30 days to reply, and thin samples were being read as failures. I widened the window to 90 days and added the exception. Dead repos are still caught by three other required checks: Maintainer alive, Repo not archived, and Repo actively used.

**Trade-offs**

The check now passes repos where maintainers may never answer outside contributors. My live run on #58 shows exactly this: "Maintainer responsive: unclear, and it counts as a pass under your exception. I sampled 8 recently updated issues. A collaborator opened every one, and none of them has a maintainer reply after that." That is a case I accept it will miss.

To check that loosening it didn't break anything, I re-ran the five misses with `--only` ("agreement: 5/5 scored items"), then did a full run. The rejects this check protects still held: "dead-repo 3/3" and "claimed 4/4", the same as before the change.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

[Answer all three:

1. The issue's fit to your interests and to the time available. 
2. What the verdict identified correctly, and what you weighed that the rubric could
   not.
3. The anticipated difficulty in claiming it.]

I want to specialize in data work, and #58 connects to that: the bias detector scans text data for patterns, which is part of checking data and model output quality.
The verdict got right that issue 58 is unclaimed, the repo is active and the scope is only a single bug. I weighed that 68 matched too but a classmate had already selected it and preffered to do something of my own.
The main difficulty is that the maintainers haven't replied to any issues recently
---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.

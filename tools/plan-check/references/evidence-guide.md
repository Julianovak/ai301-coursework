# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

## Diagnosis and grounding

- Where it lives: In an eval bundle, the cause stated anywhere in the Candidate plan section (often a "diagnosis" or "cause" line), read against the Repro evidence section (its commands, output, and failing tests) and the Issue section. In live mode, the diagnosis in the student's plan.md, read against their posted repro comment on the issue.
- What good looks like: The stated cause explains the behavior the Repro evidence actually shows, and nothing in the evidence contradicts it. Any part of the cause the evidence does not show (for example, a guess about which line is wrong) is labeled as a hypothesis.

## Scope

- Where it lives: In an eval bundle, the Candidate plan's scope statement (what will and won't change) and its list of files to touch. In live mode, the same parts of plan.md.
- What good looks like: One bounded change: the files are the ones the diagnosis points at plus their tests, and anything else (refactors, renames, new features, unrelated cleanups) is left out or explicitly deferred. A drive-by rewrite touches files or behavior the diagnosis never mentions.

## Executability

- Where it lives: In an eval bundle, the Candidate plan's files to touch and its approach. In live mode, the same parts of plan.md.
- What good looks like: The plan names the specific file(s) and the function(s) or code area to change, and the first concrete change to make. A stranger could open the named file and start, without asking what "improve the logic" means.

## Test plan

- Where it lives: In an eval bundle, the Candidate plan's test plan, read against the Repro evidence section's steps and output. In live mode, plan.md's test plan, read against the student's posted repro comment.
- What good looks like: It re-runs the repro steps (or a check that runs through the real code) and states what will be observed after the fix: specific output, or named tests passing. A vague test plan says "verify it works" or "add tests" without saying what result proves the fix. A good one also says how existing behavior will be checked (for example, the rest of the test file still passing).
## Honesty

- Where it lives: In an eval bundle, the Candidate plan's risks and unknowns, read against the claims it makes elsewhere (diagnosis, approach, expected results). In live mode, plan.md's risks/unknowns and its Deviations section after the build.
- What good looks like: Anything not yet verified is named as an assumption, risk, or open question. False confidence states an untested outcome as certain ("this will fix every case", "no side effects"). A deviation during the build is recorded under Deviations with what changed and why.


## Comms

- Where it lives: In an eval bundle, the Candidate plan comment section, read against the Thread highlights section (maintainer pointers, requested or rejected approaches, other commenters' plans) and the Repo facts section (contribution policy, AI-use disclosure, templates, discuss-before-PR asks). In live mode, comment.md, read against the issue thread on GitHub and the repo's CONTRIBUTING file and templates.
- What good looks like: The comment states this plan's own specifics (cause, change, test), follows any stated repo convention, and takes the thread into account: it uses or responds to a maintainer's pointer, rather than proposing what a maintainer already ruled out. Boilerplate ("I'll fix this soon", "same approach as above") could be pasted on any issue and fails.
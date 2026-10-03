# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

# Evidence guide: where proof lives in a reproduction package

## Environment

- Where it lives: In an eval bundle, inside the Candidate repro report section, read against the Issue section (which version, platform, or branch the issue targets). In live mode, the student's draft repro comment, read against the issue thread and the repo's setup docs (README, CONTRIBUTING, pyproject/requirements).
- What good looks like: The report names the OS and the version of the project that was run (a release version, or a commit/branch for a source checkout, plus the language runtime version when running from source). If any of these differs from what the issue targets, the report says so.

## Steps

- Where it lives: In an eval bundle, inside the Candidate repro report section (steps may be written as prose, not a list). In live mode, the steps in the draft repro comment, checked against the repo's setup docs.
- What good looks like: Starting from a fresh clone, every command needed to reach the shown output appears, in order: setup/install, then the trigger (the test, command, or input). A reader never has to invent a missing command, file, input, or setting. Judge whether the path is complete, not how many steps it has.

## Behavior shown

- Where it lives: In an eval bundle, the output, test results, traceback, or log excerpts inside the Candidate repro report section, read against the behavior described in the Issue section. In live mode, the output pasted in the draft, read against the issue body on GitHub.
- What good looks like: The artifact shows the same failing function or test and the same error type or wrong output the issue describes. An adjacent failure does not count: a different exception, a different function, or a setup/install/import error that stops before the issue's code runs. For a cannot-reproduce, the artifact shows an attempt at the issue's described conditions (the issue's own trigger when it gives one), and the described behavior did not appear. Saying "same here" with no artifact is not evidence.

## Honesty

- Where it lives: The stated result in the Candidate repro report section ("reproduced", "cannot reproduce", "partial", or a summary), read against the artifacts found under Behavior shown.
- What good looks like: The main result is visible in the artifacts; a side observation given with its exact command does not need pasted output. "Reproduced" has output showing the failure; "cannot reproduce" has output showing the trigger ran cleanly; any cause or fix mentioned is labeled as a guess unless evidence is shown. A report that claims more than its artifacts show fails, however confident it sounds. An evidenced cannot-reproduce passes.

## Comms

- Where it lives: The Candidate claim comment and Candidate repro report sections, read against the Issue section and against the contribution policy and bug reports lines in the Repo facts section. In live mode, the draft comments read against the issue thread and the repo's CONTRIBUTING file, issue/PR templates, and any AI-use policy.
- What good looks like: The claim names the issue by number or its specific behavior and promises only to investigate and report back, with no fix, PR, or date promised. If the contribution policy requires disclosing AI assistance, every comment includes a disclosure; if it says nothing, there is nothing to disclose. Specific-and-honest names this issue's details; boilerplate ("I'd like to work on this!", "+1", "same here") could be pasted on any issue.
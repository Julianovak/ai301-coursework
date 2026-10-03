# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Claim is specific and promises only investigation | The claim comment's text | The claim identifies the issue by number or by its specific behavior, and commits only to investigating/reproducing and reporting back; it does not promise a fix, a PR, or a date | required |
| Environment recorded | The repro report's environment record | States the OS and the version of the project that was run (a release version, or a commit/branch for a source checkout, plus the language runtime version when running from source | required |
| Steps followable | The repro report's steps, read as if starting from a fresh clone | A reader can get from a fresh clone to the shown output by running the stated commands in order, without inventing a missing command, file, or input | required |
| Behavior matches issue | If reproduction is claimed: the artifact shows the same failing function/test and the same error or wrong output the issue describes; a different error, a different function, or a setup/install failure does not pass. If cannot-reproduce is claimed: the artifact shows an attempt at the issue's described conditions (using the issue's own command, test, or input when it gives one), says which scenario was tested, and shows the described behavior did not appear | required |
| Outcome stated honestly | The main stated outcome (reproduced, cannot reproduce, or partial) is what the artifacts show. Fail if the main outcome has no supporting output, or a root cause is asserted as fact without evidence. A side observation described with its exact command but no pasted output does not fail the package. An evidenced cannot-reproduce passes | required |
| Repo conventions respected | The contribution-policy line in the repo-facts block, read against the claim and repro comment text | If the policy requires disclosing AI assistance, every comment in the package includes a disclosure; any other stated requirement for comments is followed; a policy that says nothing passes | required |
| Expected vs. observed stated | The repro report's result section | The report states both what should happen and what actually happened | preferred |

## Verdict rule

Accept (ready to post) if every `required` check passes. A `required` check graded `unclear` whose evidence begins `not yet applicable:` (a repro check on a claim-only draft) is skipped and does not count as a fail. Any other `required` check graded `unclear` counts as fail, because a package should only be posted when its proof is visible in it. `preferred` checks never change the verdict.
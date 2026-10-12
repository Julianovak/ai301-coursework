# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

1. Read the Issue section first. Note the behavior the issue reports and any expected behavior it states.
2. Read the Repro evidence section second. Note exactly what it shows: the commands run, the output, which tests fail, and what the expected-vs-actual difference is. This is the fixed point every later check is measured against, so it is read before the plan, which keeps the plan's own framing from shaping what the evidence "shows".
3. Read the Thread highlights section third. Note any maintainer guidance: pointers to code, a requested or rejected approach, "please don't" instructions, and other commenters' plans.
4. Read the Repo facts section fourth. Note the contribution policy and any other stated convention (AI-use disclosure, discuss-before-PR, templates).
5. Read the Candidate plan fifth. Note its stated cause, scope, files to touch, approach, test plan, and risks/unknowns, wherever in the plan they appear.
6. Read the Candidate plan comment last, since it is checked against everything above.

## Evidence gathering

1. Diagnosis fits the evidence: from the Candidate plan, record its stated cause in one line. From the Repro evidence, record the observed output and failing tests that the cause must explain.
2. Targets the cause, not the symptom: from the Candidate plan, record the proposed change (what code changes, and where). Record whether it changes the code the diagnosis points at, or only tests, error handling, or the exact repro input.
3. Scope is bounded: from the Candidate plan, record every file and change it says it will make, and anything it says it will not change.
4. A stranger could start: from the Candidate plan, record the named files, functions or code areas, and the first concrete change.
5. Test plan proves the fix: from the Candidate plan, record its test plan steps and the expected result it states. From the Repro evidence, record the original repro steps to compare against.
6. Unknowns stated honestly: from the Candidate plan, record every claim stated as certain, and every item labeled as a risk, assumption, or unknown.
7. Comment respects thread and conventions: from the Candidate plan comment, record its text. From the Thread highlights, record any maintainer guidance. From the Repo facts, record the contribution policy and stated conventions.
8. Guards against regressions: from the Candidate plan's test plan, record any step that checks existing behavior.

If a fact is not in the package, record "not found" for it rather than guessing.
## Check execution

1. Run the checks in rubric order, one at a time, using only the evidence recorded for that check.
2. For each check, apply its pass condition exactly as written and grade it `pass`, `fail`, or `unclear`. Quote the line(s) from the package that decided it.
3. Grade `fail` when the evidence shows the condition is broken (for example, the plan edits the failing tests' expected values).
4. Grade `unclear` only when the recorded evidence is "not found" and the condition cannot be decided either way. Do not grade `unclear` because a fact is worded differently or appears in a different part of the plan than expected; look for it across the whole Candidate plan first.
5. Judge the outcome, not the layout: a plan without a "Risks" heading can still pass Unknowns stated honestly if nothing unverified is stated as certain.
6. A check may be graded from its recorded evidence alone, without re-reading the whole package, unless the recorded evidence is "not found".

If a fact is not in the package, record "not found" for it rather than guessing.

## Verdict assembly

1. Apply the rubric's verdict rule: accept only if every `required` check is `pass`.
2. Any `required` check graded `fail` or `unclear` makes the verdict reject.
3. `preferred` checks are reported but never change the verdict.
4. For a reject, quote the deciding check's name and the package line that failed it. For an accept, state that all required checks passed.
5. End the output with the JSON block in the format SKILL.md specifies, with each check's name, grade, and quoted evidence, and the verdict.
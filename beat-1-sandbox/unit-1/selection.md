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

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/57

**Verdict output**

```json
[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/57",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "COLLABORATOR Aburke225 opened+labeled issue 2026-09-10; human-authored main commit 2026-09-16 (6 days before capture)"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "archived: false; newest default-branch commit 2026-09-16, within 180 days"},
      {"name": "bounded-scope", "grade": "pass", "evidence": "Single fix in tech_detector.py excluding node_modules/ and build/; two named failing tests; no tracking list or design debate"},
      {"name": "unclaimed", "grade": "pass", "evidence": "assignees: []; comments: 0; only open PR in repo is #74 targeting #60"},
      {"name": "ai-policy", "grade": "pass", "evidence": "No CONTRIBUTING.md/AI_POLICY.md (404); PR template requires CI and tests only, no AI ban"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/56",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "COLLABORATOR Aburke225 opened+labeled issue 2026-09-10; human-authored main commit 2026-09-16"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "archived: false; newest default-branch commit 2026-09-16, within 180 days"},
      {"name": "bounded-scope", "grade": "pass", "evidence": "StructuralChunker.chunk() returns [] for heading-less docs; one named failing test; single-function fallback"},
      {"name": "unclaimed", "grade": "pass", "evidence": "assignees: []; comments: 0; two 'referenced' events point at commits in vchlinh/ai301-coursework, not a PR on this repo"},
      {"name": "ai-policy", "grade": "pass", "evidence": "No CONTRIBUTING.md/AI_POLICY.md (404); PR template has no AI restriction"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/58",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "COLLABORATOR Aburke225 opened+labeled issue 2026-09-10; human-authored main commit 2026-09-16"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "archived: false; newest default-branch commit 2026-09-16, within 180 days"},
      {"name": "bounded-scope", "grade": "pass", "evidence": "Widen regex patterns in bias_detector.py; 9 named failing tests in one test file; no umbrella checklist, no core-internals warning"},
      {"name": "unclaimed", "grade": "pass", "evidence": "assignees: []; comments: 0; no linked or mentioned PR"},
      {"name": "ai-policy", "grade": "pass", "evidence": "No CONTRIBUTING.md/AI_POLICY.md (404); PR template has no AI restriction"}
    ],
    "verdict": "accept"
  }
]
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

1. `--limit 3` smoke run, 3/3. No rubric changes. This only confirmed the harness parsed my table and produced verdicts.
2. Full run, 16/20. Below the bar and the category floor was unmet, `categories: claimed 4/4  clear-accept 6/8  dead-repo 3/3  policy 0/1  scope 3/4`. I had cut the contribution-policy check to keep the rubric minimal, which lost the policy category outright. issue-01 and issue-19 were false rejects, both `failed: bounded-scope`.
3. Full run, 17/20. I added the ai-policy check back and deleted the clause in bounded-scope that failed issues open more than a year with two or more closed unmerged PRs. policy went to 1/1 and issue-19 flipped to accept, but issue-15 became a false accept, so scope fell from 3/4 to 2/4.
4. Full run, 18/20, `bar: 18/20: PASS`. I narrowed the umbrella clause in bounded-scope to require sub-items that are separate work split across PRs or contributors, and added that a detailed spec for a single deliverable passes. issue-01 flipped to accept and clear-accept went to 8/8.
5. Final run with `--save-run eval-run.txt`, 18/20. No rubric changes after run 4.

**Issue analysis**

issue-15 (zulip/zulip#19589). My rubric graded it accept. The gold label is reject.

Every required check passed. The repo is alive, with a default-branch commit on 2026-08-03 and a first-response sample showing `#39859 (opened 2026-07-31): 2.6 days`. It is not archived and released 12.1 on 2026-06-26. The issue carries `good first issue`, has no assignee, and its linked PRs are `zulip/zulip#20840 (closed); zulip/zulip#23123 (closed)`, which my unclaimed check treats as abandoned attempts rather than active claims. The body is one bounded change, separating the slash command into a `command` field and leaving the message body in `text`, with no umbrella structure and no unsettled design debate.

What my rubric cannot see is the history. The issue was opened on 2021-08-18 and has 97 comments, most of them zulipbot claiming and then releasing contributors, for example `Hello @LoganNiswander, you have been unassigned from this issue because you have not updated this issue or any referenced pull requests for over 14 days.` The same cycle repeats for leighadennis, blackbird7112, BrianMcDowell, Kaustubhkongile, ikrambil, SamChen41 and souvik150. Five years open, two abandoned PRs and roughly eight lapsed claims is exactly what the evidence guide means by "an issue open for years with several abandoned attempts (closed, unmerged PRs in its history) is telling you something about its real difficulty." My rubric reads each of those signals in isolation and finds nothing disqualifying in any one of them.

**Check rationale**

> Fails if any of these hold. The issue is explicitly an umbrella or tracking issue, meaning it lists sub-items that are separate pieces of work meant to be split across multiple PRs or contributors, shown by a tracking label or a checklist of links to other issues. The thread shows an open design debate with no maintainer decision. A maintainer says the fix requires changes to core internals. The issue is a usage or support question rather than a change request. Otherwise pass. A terse body, a checklist of acceptance criteria, or a bug report without repro steps is not a fail by itself. A detailed spec that breaks a single deliverable into sections of the same change, such as a new page plus the existing pages that link to it, is one bounded piece of work and passes.

The last two sentences exist because my first version failed issue-01 (conda/conda#16475) on its structure rather than its size. That issue has `### Add a new task page`, `### Update manage-pkgs.rst`, `### Update pip-interoperability.rst` and `### Update new-features.md` as separate headed sections, which my umbrella clause read as sub-items. They are not separate work. They are one docs change plus the pages that point at it. The evidence guide says to "grade the size of the work being asked for, not the polish of the writeup," so the check now requires a genuine split across PRs or contributors, and names the single-deliverable-with-sections case as a pass.

**Trade-offs**

It gives up the abandoned-attempt signal. My run 2 rubric also failed any issue open more than a year with two or more closed unmerged PRs, and that clause is what caught issue-15. Removing it was deliberate. It was also rejecting issue-19, a gold accept, and with it in place run 2 sat at 16/20 with clear-accept at 6/8. Without it, run 4 reached 18/20 with clear-accept at 8/8 and issue-15 as one of the two remaining misses. I took the version that never misses a clear accept, and I accept that it cannot see a long, stalled history.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

1. Fit and time. #57 is Python backend tooling, which is the direction I want to push in. I work mostly in TypeScript and Java, so this is unfamiliar-codebase reading without also being a framework I have never touched. The fix is path filtering in one module, with two named failing tests and a deterministic expected output of 'Python', so I can tell when I am done. That matters with Unit 2 starting immediately.

2. What the verdict got right, and what I weighed on top. The rubric confirmed the mechanical facts, that the repo is not archived, that a human commit landed on main six days before the run, that there is no assignee and no linked PR, and that no policy blocks AI-assisted work. What it could not weigh is that #58, which it also accepted, has nine failing tests and asks for regex patterns that "match natural phrasings." That is open-ended judgment work where over-matching is easy and there is no single correct answer. My rubric graded it bounded because it is one module with no design debate, and by its own terms that is right. I still ranked it last.

3. Claiming it. Low friction expected. Zero comments, no assignee, and the only open PR in the repo is #74, which targets #60. The real risk is a classmate claiming it before I post in Unit 2. The Path Review house rule says shared issues cost nobody anything and credit attaches to the PR I open, so it would not block me, but I would rather not duplicate work.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.

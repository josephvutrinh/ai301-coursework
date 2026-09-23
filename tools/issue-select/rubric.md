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
| maintainer-alive | "last 5 default-branch commits" and "maintainer first-response sample" under Repo facts; author_association on comments in this issue's thread | Within 90 days of the capture date (today in live mode), at least one of these is true. A default-branch commit was authored by a human, or was made by a bot merging a human's PR. Someone with OWNER, MEMBER, or COLLABORATOR association commented on this issue or on an issue in the first-response sample. Commits authored only by accounts ending in [bot], with no human PR behind them, do not count. | required |
| repo-in-use | "archived:" on the repo line; "latest release" and "last 5 default-branch commits" under Repo facts | Archived is false, and either the latest release is within 365 days of the capture date or the newest default-branch commit is within 180 days. Archived true is always a fail. Pushes to non-default branches alone do not pass this check. | required |
| bounded-scope | issue body and full comment thread | Fails if any of these hold. The issue is an umbrella or tracking issue listing sub-items meant to be split into separate work. The thread shows an open design debate with no maintainer decision. A maintainer says the fix requires changes to core internals. The issue is a usage or support question rather than a change request. Otherwise pass. A terse body, a checklist of acceptance criteria, or a bug report without repro steps is not a fail by itself. | required |
| unclaimed | "this issue: assignees:" and "linked PRs:" under Repo facts; PRs mentioned and claim comments in the comment thread | Fails if any of these hold. The issue has an assignee and no maintainer comment after the assignment says it is open again. There is an open PR for it, either linked or mentioned in the thread. Someone posted a claim comment ("I'll take this", "can I work on this", "working on this") within 30 days of the capture date and has not said they are dropping it. When the sidebar and the thread disagree, the thread wins. Closed, unmerged PRs are abandoned attempts and do not fail this check. | required |
| ai-policy | "contribution policy" line under Repo facts (CONTRIBUTING.md, AI_POLICY.md, AI_USAGE_POLICY.md, PR templates) | Fails only if the policy bans AI-generated or AI-assisted contributions outright. Disclosure, testing, understanding, or human-review requirements pass. No stated policy passes. An AGENTS.md file passes. | required |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict, they
rank accepted issues; unclear counts as fail." -->

Accept if every required check passes. Reject if any required check fails. Unclear on unclaimed or ai-policy counts as pass, since the absence of a claim or a policy is itself the passing signal. Unclear on maintainer-alive, repo-in-use, or bounded-scope counts as fail.

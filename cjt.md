Make a copy of this template file. Rename the file to include your initials, e.g., slh.md. 

Edit only your markdown file please. We are not learning how to resolve merge conflicts yet. Insert AI answer to your daily questions after the question. Use markdown to format this file. 

Edit one daily question each of five days. Each day issue the following commands. 

    git pull
    make your edits
    git add -A
    git commit -m ‘Day X answered’
    git push
    git status

You can double-check a successful commit and push at [GitHub repo](https://github.com/sean-humpherys/cidm4390-practice-pull-commit-push)

## Day 1’s Question

If two coders, working in the main branch, modify the same file commit and push at different times, what are the consequences? Please put your answer into a markdown format.

## Day 1’s Answer
Two Developers Modifying the Same File on main
Short Answer

It depends on what each person changed and who pushes second. The first push always succeeds. The second push is rejected until that developer integrates the first person's changes. Whether that integration is painless or requires manual conflict resolution depends on whether the edits overlap.

Scenario
Alice and Bob both pull main and start from the same commit (A).
Both edit app.js and commit locally.
Alice pushes first. Her commit is accepted.
Bob pushes later.
        Alice's commit
       /
A ---- B   (origin/main after Alice pushes)
 \
  C        (Bob's local commit, based on A)
What Happens to Bob's Push

Git rejects it as a non-fast-forward update:

! [rejected]        main -> main (fetch first)
error: failed to push some refs to 'origin'
hint: Updates were rejected because the remote contains work that you do
hint: do not have locally.

This is a safety mechanism. Git won't let Bob overwrite Alice's work.

Two Possible Outcomes After Bob Pulls
Case 1: Changes don't overlap (auto-merge)

If they edited different parts of the file (e.g., different functions or distant lines), Git merges them automatically.

With git pull (merge): creates a merge commit.
With git pull --rebase: replays Bob's commit on top of Alice's, giving a linear history.
Bob can then push successfully.
Case 2: Changes overlap (merge conflict)

If they edited the same lines (or adjacent lines), Git can't decide which version wins and stops:

CONFLICT (content): Merge conflict in app.js
Automatic merge failed; fix conflicts and then commit the result.

The file will contain conflict markers:

<<<<<<< HEAD
Bob's version of the line
=======
Alice's version of the line
>>>>>>> origin/main

Bob must:

Open the file and decide what the final content should be (keep one, the other, or a combination).
Remove the conflict markers.
git add app.js
git commit (or git rebase --continue if rebasing).
git push
Consequences Summary
Aspect	Impact
Data loss	None, as long as nobody force-pushes
Second pusher	Must pull/integrate before pushing
Auto-merge possible?	Yes, if edits are in different regions
Manual resolution needed?	Yes, if edits overlap
History	Merge commit (merge) or linear history (rebase)
Semantic bugs	Possible even with a clean merge (see below)
Hidden Risks
Clean merge ≠ correct code. Git merges text, not logic. If Alice renames a function and Bob adds a call to the old name in a different part of the file, the merge succeeds but the code is broken.
Force-pushing (git push --force) would overwrite Alice's commit on the remote and destroy her work from the shared history. Avoid this on main.
Wrong conflict resolution can silently discard someone's changes.
Broken main: pushing unverified merges directly to main can break the build for the whole team.
Best Practices
Pull frequently (git pull --rebase) before starting work and before pushing.
Commit small and often to reduce the size of conflicts.
Use feature branches and pull requests instead of committing directly to main.
Enable branch protection on main (required reviews, required CI checks).
Run tests after merging before pushing.
Communicate about who's working on which files.

## Day 2’s Question

What are best practices regarding how often to commit and push, including recommended frequency? Please put your answer into a markdown format.

## Day 2's Answer

Git Commit and Push Best Practices
Commit Frequency

Commit early and often, in small logical units. There’s no universal number, but a good rule of thumb is to commit every time you complete one coherent, working change.

Guideline	Recommendation
Typical cadence	Every 15 to 60 minutes of active work, or whenever a logical step is done
Size	Small enough to describe in one sentence; large enough to stand on its own
Per day	Several commits is normal; a full day with only one commit is a warning sign
State	Ideally each commit builds and passes tests
Commit when you have:
Finished a single logical change (a bug fix, a function, a refactor step)
Reached a stable checkpoint before trying something risky
Completed a change that can be described without using “and”
Avoid:
Giant commits that mix unrelated changes (feature + refactor + formatting)
Tiny meaningless commits like “fix typo” repeated ten times (squash these before sharing)
Broken commits that leave the build failing, especially on shared branches
Push Frequency

Push at least once per day, and more often when collaborating. Unpushed work exists on only one machine and is invisible to your team.

Situation	Suggested push cadence
Solo feature branch	At least daily, and at the end of every work session
Team feature branch	After each meaningful commit or a few times a day
Shared or main branch	Only after tests pass and the change is review-ready
Long-running work	Push often as backup, and rebase or merge from main regularly
Benefits of frequent pushing
Backup against laptop failure or loss
Visibility so teammates can see progress and give early feedback
Smaller merge conflicts because branches diverge less
Easier CI feedback on every push
Commit Message Tips
Use the imperative mood: Add login validation, not Added login validation
Keep the subject line to about 50 characters, with a blank line before the body
Explain why in the body, not just what changed
Reference issues or tickets where relevant (Fixes #123)
text
Add rate limiting to login endpoint

Prevents brute-force attempts by limiting each IP to 5 attempts
per minute. Returns 429 with a Retry-After header.

Fixes #482
Workflow Recommendations
Work on a feature branch, not directly on main.
Commit locally as often as you like to create safe checkpoints.
Clean up before sharing: use git rebase -i or squash to tidy messy WIP commits (only on branches that others haven’t based work on).
Pull or rebase from main frequently (at least daily) to avoid large conflicts.
Push regularly, then open a pull request when ready for review.
Never force-push to shared branches unless the team has agreed to it. Prefer --force-with-lease on your own branches.
Team Conventions Matter

Practices vary by team and workflow:

Trunk-based development: very small commits, merged to main multiple times per day behind feature flags
Feature-branch / PR workflow: more flexibility locally, with commits squashed or tidied at merge
Squash-merge teams: individual commit granularity matters less on the branch, but still helps you and reviewers during development

Always follow your team’s documented conventions where they exist.

## Day 3’s Question

Explain branches in git and their best practices? Please put your answer into a markdown format.

## Day 4’s Question

What is the difference between git pull and git fetch? My professor advises using git pull over git fetch? Can you put your answer into a markdown format please.

## Day 5’s Question

What are alternatives to github?Please put your answer into a markdown format.

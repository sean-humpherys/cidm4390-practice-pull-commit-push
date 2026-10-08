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

## Day 3’s Question

Explain branches in git and their best practices? Please put your answer into a markdown format.

## Day 4’s Question

What is the difference between git pull and git fetch? My professor advises using git pull over git fetch? Can you put your answer into a markdown format please.

## Day 5’s Question

What are alternatives to github?Please put your answer into a markdown format.

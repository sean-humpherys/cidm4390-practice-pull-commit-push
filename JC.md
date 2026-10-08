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

Two Developers Editing the Same File on main
Scenario

Alice and Bob both clone the repository at commit C1. Each edits app.js, commits locally, and pushes, Alice first and Bob later.

            Alice: C1 ── A1   (pushed first)
           /
remote: C1
           \
            Bob:   C1 ── B1   (pushed second)
1. The first push succeeds

Alice's push goes through normally. The remote main now points to A1.

2. The second push is rejected

Bob's local history doesn't contain A1, so his push would not be a fast-forward. Git refuses it:

! [rejected]        main -> main (fetch first)
error: failed to push some refs to 'origin'
hint: Updates were rejected because the remote contains work that you do not have locally.

Nothing is lost at this point. Git protects Alice's work by default.

3. Bob must integrate Alice's changes first

Bob runs either:

bash
git pull            # fetch + merge (creates a merge commit)
# or
git pull --rebase   # replays B1 on top of A1 (linear history)

What happens next depends on what lines each person changed:

Situation	Result
Changes are in different parts of the file	Git auto-merges cleanly. Bob then pushes successfully.
Changes touch the same or adjacent lines	Merge conflict. Git stops and marks the file.
One person deleted the file, the other edited it	Modify/delete conflict that must be resolved manually.
4. Resolving a conflict

Git inserts conflict markers into the file:

javascript
<<<<<<< HEAD
const timeout = 5000;   // Bob's version
=======
const timeout = 3000;   // Alice's version
>>>>>>> origin/main

Bob must:

Edit the file to the correct final content and remove the markers.
Stage it with git add app.js.
Finish with git commit (merge) or git rebase --continue (rebase).
Push with git push.
Hidden risks
⚠️ Force pushing destroys work

If Bob "fixes" the rejection with git push --force, the remote is overwritten with his history and Alice's commit A1 disappears from main. It can only be recovered from Alice's local repo or the reflog.

⚠️ Semantic conflicts

Git merges text, not meaning. A clean auto-merge can still break the code. For example, Alice renames a function while Bob adds a new call to its old name. Git sees no conflict, but the build fails.

⚠️ Careless conflict resolution

A rushed resolution ("accept mine" for everything) can silently discard the other developer's changes.

⚠️ Messy history

Repeated git pull merges on main produce many "Merge branch 'main' of origin" commits, which make the history harder to read.

⚠️ Broken main

Because everyone works directly on main, any bad merge immediately affects the whole team.

Best practices to avoid these problems
Pull before you start, and before you push: git pull --rebase.
Commit and push small changes often so divergence stays small.
Use feature branches and pull requests instead of committing directly to main.
Protect main (branch protection rules): require reviews, block force pushes.
Run CI on every merge to catch semantic conflicts.
Communicate when two people need to work on the same area of code.
If you must override remote history, use git push --force-with-lease. It refuses to push if the remote has commits you haven't seen.

## Day 2’s Question

What are best practices regarding how often to commit and push, including recommended frequency? Please put your answer into a markdown format.

## Day 3’s Question

Explain branches in git and their best practices? Please put your answer into a markdown format.

## Day 4’s Question

What is the difference between git pull and git fetch? My professor advises using git pull over git fetch? Can you put your answer into a markdown format please.

## Day 5’s Question

What are alternatives to github?Please put your answer into a markdown format.

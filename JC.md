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

Git Commit & Push Best Practices
Core Principle

Commit often, perfect later, publish once. Commits are cheap, local, and private until you push. Use them freely as save points, then tidy them up before sharing.

How Often to Commit
Recommended Frequency
Every 15–60 minutes of active work is a common rule of thumb.
More precisely: commit whenever you complete one logical unit of change. Time is a rough guide; the logical unit is what matters.
Good Moments to Commit
A function, method, or small feature works.
A bug is fixed (ideally with its test).
Tests pass after a change.
Before starting a risky refactor or experiment.
Before switching tasks, branches, or stopping for the day.
After a rename or move. Keep these separate from content changes so diffs stay readable.
What Makes a Good Commit
Principle	Explanation
Atomic	One logical change per commit. Don’t mix a bug fix with formatting cleanup.
Buildable	Each commit on a shared branch should compile and pass tests. This keeps git bisect useful.
Small	Easier to review, revert, and understand. Aim for diffs a reviewer can read in a few minutes.
Well-described	Clear message explaining what and why (see below).
Signs You’re Committing Too Rarely
Commit messages like “lots of changes” or “WIP stuff.”
Diffs touching dozens of unrelated files.
Fear of losing hours of work if something goes wrong.
Difficulty writing a single-sentence summary of the commit.
Signs You’re Committing Too Often (on shared history)
Long strings of “fix typo,” “oops,” “try again” commits.
Commits that break the build mid-sequence.

Fix: Squash or rebase these locally (git rebase -i) before pushing or merging.

How Often to Push
Recommended Frequency
At least once per day for work in progress, even on a feature branch.
Whenever a coherent set of commits is ready for others to see, review, or test.
Before ending your workday. Your local machine is not a backup.
Push to Your Feature Branch Freely
Pushing to your own branch is low-risk. It backs up your work and enables early feedback and CI runs.
Open a draft pull request early to show progress and get feedback.
Be Deliberate About Pushing to Shared Branches
Don’t push directly to main or develop unless your team’s workflow allows it.
Make sure the code builds and tests pass before pushing to anything others depend on.
Never force-push to a shared branch that others have pulled. On your own branch, prefer git push --force-with-lease over --force.
Workflow-Specific Guidance
Workflow	Commit Frequency	Push / Merge Frequency
Trunk-based development	Many small commits per day	Integrate into trunk at least daily, often several times a day; use feature flags for unfinished work
GitHub Flow / feature branches	Frequent local commits	Push branch daily; merge via PR when complete. Keep branches short-lived (ideally under 1–3 days)
Git Flow	Frequent local commits	Push feature branches daily; merge to develop per feature, to main per release
Solo / personal projects	Frequent	Push at least daily for backup

General guidance: Long-lived branches cause painful merge conflicts. The longer a branch lives apart from the main line, the harder integration becomes. Sync with the main branch (git pull --rebase or merge) at least daily.

Commit Message Guidelines
Short summary in imperative mood (≤50 chars)

Optional body explaining what changed and why, wrapped
at ~72 characters. Reference issues if relevant.

Fixes #123
Use the imperative mood: “Add login validation,” not “Added” or “Adds.”
Explain why in the body. The diff already shows what.
Consider 
Conventional Commits (feat:, fix:, docs:, etc.) if your team uses automated changelogs or versioning.
Quick Checklist Before Pushing
 Each commit is a single logical change
 Code builds and tests pass
 No secrets, credentials, or large binaries included
 WIP/fixup commits are squashed (if pushing to a shared or review branch)
 Commit messages are clear
 Branch is up to date with the target branch
TL;DR
Action	Recommended Frequency
Commit	Every logical unit of work, roughly every 15–60 minutes
Push (feature branch)	At least daily, and whenever you want backup or feedback
Integrate into main	At least daily for trunk-based teams; per completed feature otherwise. Keep branches short-lived
Sync with main	At least daily

## Day 3’s Question

Explain branches in git and their best practices? Please put your answer into a markdown format.

Git Branches: Concepts and Best Practices
What Is a Branch?

A branch in Git is a lightweight, movable pointer to a commit. It lets you work on new features, bug fixes, or experiments separately from the main codebase.

When you create a branch, Git doesn’t copy files. It creates a new pointer to the current commit.
As you make commits on a branch, the pointer moves forward automatically.
HEAD is a special pointer that tells Git which branch (or commit) you’re currently on.
          feature-login
               ↓
A --- B --- C --- D
       \
        E --- F
              ↑
            main (HEAD)
Why Use Branches?
Isolation: Work on a feature without breaking stable code.
Parallel development: Multiple people or tasks can progress at once.
Safe experimentation: Delete a failed experiment without consequences.
Code review: Branches pair naturally with pull/merge requests.
Essential Branch Commands
Task	Command
List local branches	git branch
List all branches (incl. remote)	git branch -a
Create a branch	git branch <name>
Switch to a branch	git switch <name>
Create and switch	git switch -c <name>
Rename current branch	git branch -m <new-name>
Delete a merged branch	git branch -d <name>
Force-delete a branch	git branch -D <name>
Push branch to remote	git push -u origin <name>
Delete a remote branch	git push origin --delete <name>
Merge a branch into current	git merge <name>
Rebase current onto another	git rebase <name>

git switch is the modern alternative to git checkout for changing branches. git checkout still works but does many unrelated things.

Merging vs. Rebasing
Merge

Combines histories and creates a merge commit.

bash
git switch main
git merge feature-login
✅ Preserves full, true history
✅ Safe for shared branches
❌ Can produce a cluttered history
Rebase

Replays your commits on top of another branch, producing a linear history.

bash
git switch feature-login
git rebase main
✅ Clean, linear history
❌ Rewrites commit hashes
⚠️ Never rebase branches others are working on
Squash Merge

Combines all of a branch’s commits into a single commit on the target branch, which keeps main tidy. It’s common in pull-request workflows.

Common Branching Strategies
1. GitHub Flow (simple, popular)
main is always deployable.
Create a short-lived branch for each change.
Open a pull request, review, merge, deploy.

Best for: Web apps, continuous deployment, small to medium teams.

2. Git Flow (structured)
main: production releases
develop: integration branch
feature/*, release/*, hotfix/*: supporting branches

Best for: Projects with scheduled, versioned releases. It’s often considered heavy for modern CI/CD.

3. Trunk-Based Development
Everyone commits to main (the “trunk”) frequently, using very short-lived branches (hours to a day or two).
Unfinished work is hidden behind feature flags.

Best for: Mature teams with strong automated testing and CI.

Best Practices
Naming
Use clear, descriptive names with a type prefix:
feature/user-authentication
fix/login-timeout
hotfix/payment-crash
chore/update-dependencies
Include ticket IDs when relevant: feature/JIRA-123-add-search
Use lowercase and hyphens; avoid spaces and special characters.
Keep Branches Short-Lived
Long-running branches drift from main and cause painful merge conflicts.
Aim to merge within days, not weeks.
Break large features into smaller, mergeable pieces.
Sync Frequently

Regularly pull in changes from main:

bash
git fetch origin
git rebase origin/main   # or: git merge origin/main
Protect Important Branches

On your hosting platform (GitHub, GitLab, Bitbucket):

Block direct pushes to main.
Require pull request reviews.
Require passing CI checks before merging.
Disallow force-pushes.
One Purpose per Branch
Each branch should address a single feature, fix, or task.
This makes reviews easier and reverts safer.
Write Good Commits
Make small, logical commits with meaningful messages.
Clean up local history (e.g., git rebase -i) before sharing, not after.
Clean Up After Merging
Delete merged branches locally and remotely.
Prune stale remote-tracking branches:
bash
git fetch --prune
Never Rewrite Shared History
Avoid rebase or push --force on branches others use.
If you must force-push your own branch, prefer the safer option:
bash
git push --force-with-lease
Quick Example Workflow
bash
# 1. Start from an up-to-date main
git switch main
git pull

# 2. Create a feature branch
git switch -c feature/add-search

# 3. Work and commit
git add .
git commit -m "Add search bar component"

# 4. Stay current with main
git fetch origin
git rebase origin/main

# 5. Push and open a pull request
git push -u origin feature/add-search

# 6. After merge, clean up
git switch main
git pull
git branch -d feature/add-search
Summary
Branches are cheap pointers, so use them freely.
Pick a strategy that fits your team (GitHub Flow suits most teams).
Keep branches small, focused, short-lived, and well-named.
Protect main, sync often, and never rewrite shared history.

## Day 4’s Question

What is the difference between git pull and git fetch? My professor advises using git pull over git fetch? Can you put your answer into a markdown format please.

## Day 5’s Question

What are alternatives to github?Please put your answer into a markdown format.

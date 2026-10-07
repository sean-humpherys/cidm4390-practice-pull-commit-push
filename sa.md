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


When the second coder attempts to push their changes to the remote main branch, Git will intervene to prevent the first coder's work from being overwritten. The sequence of events depends entirely on which lines of the file were modified.

1. The Push Rejection
The second coder's git push will fail. Git will return a rejected (non-fast-forward) error because the remote repository contains commits (from the first coder) that do not exist in the second coder's local repository.

2. The Required Pull
To proceed, the second coder must integrate the remote changes into their local environment, typically by running git pull (or git fetch followed by git merge or git rebase).

3. The Integration Attempt
When the second coder pulls the remote changes, Git attempts to combine both sets of modifications into the single file. This results in one of two outcomes:

Automatic Merge (Different Lines): If the coders edited entirely different, non-adjacent sections of the file, Git will automatically merge the changes. It generates a new "merge commit" combining both histories. The second coder can then immediately push to the remote repository.

Merge Conflict (Same Lines): If both coders edited the exact same line, or lines immediately adjacent to each other, Git cannot determine which version is correct. It halts the merge process, marks the file as conflicted, and waits for human intervention.

4. Conflict Resolution (If Applicable)
If a merge conflict occurs, the second coder is responsible for fixing it before they can push. They must:

Open the conflicted file and locate the Git conflict markers (<<<<<<< HEAD, =======, >>>>>>> [commit hash]).

Manually edit the code to reflect the correct final state (keeping Coder A's changes, Coder B's changes, or a combination of both).

Delete all conflict markers.

Stage the resolved file (git add).

Commit the resolution (git commit).

Push the finalized, combined code to the remote repository (git push).

## Day 2’s Question

What are best practices regarding how often to commit and push, including recommended frequency? Please put your answer into a markdown format.
1. Committing Code

A commit is a snapshot of your local repository at a specific point in time.

Best Practices

Make Atomic Commits: Each commit should encompass a single, logical change. If you fixed a bug and added a new feature, those should be two separate commits. This makes it easier to track changes, review code, and revert if something goes wrong.

Write Clear Commit Messages: Use the imperative mood (e.g., "Add user authentication," not "Added user authentication"). The first line should be a concise summary (under 50 characters), followed by a blank line and a more detailed explanation if necessary.

Don't Commit Broken Code: While you might save intermediate steps locally, try to ensure that the code compiles and passes basic tests before you finalize a commit, especially if you are about to push it.

Separate Configuration from Code: Don't commit local configuration files or secrets (use .gitignore).

Recommended Frequency

Commit Often: You should be committing multiple times a day.

Rule of Thumb: Commit every time you complete a small unit of work. This could be anywhere from every 15 minutes to every 2 hours, depending on the complexity of the task.

2. Pushing Code

Pushing syncs your local commits to a remote server (like GitHub, GitLab, or Bitbucket), making them available to your team and serving as a backup.

Best Practices

Push to Feature Branches: Always do your active development on a feature branch, not directly on main or develop.

Ensure Tests Pass Before Pushing to Shared Branches: If you are pushing to a branch that others pull from, make absolutely sure your code doesn't break the build.

Rebase or Merge Before Pushing: If others have pushed changes to the remote branch, pull those changes and integrate them (via merge or rebase) before pushing your own.

Recommended Frequency

Push at Least Daily: At a minimum, push your feature branch to the remote repository at the end of every workday. This ensures your work is backed up in case your local machine fails.

Push at Milestones: Push your code when you have reached a logical milestone, are ready to open a Pull Request (PR), or need another developer to review or collaborate on your specific branch.

Rule of Thumb: Most developers push 1 to 3 times a day.
## Day 3’s Question

Explain branches in git and their best practices? Please put your answer into a markdown format.
A Git branch is a lightweight, movable pointer to a specific commit. It creates an isolated parallel workspace where you can develop features, fix bugs, or experiment safely without affecting the stable main codebase.

Best Practices
Adopt a Naming Convention: Use clear prefixes to indicate the branch's purpose (e.g., feature/login-page, bugfix/header-alignment, hotfix/api-crash).

Keep Them Short-Lived: Merge branches back into your main branch as quickly as possible—ideally within a few days—to prevent massive merge conflicts later.

One Branch, One Task: Keep branches strictly focused on a single feature or fix. Do not mix unrelated changes.

Sync Frequently: Regularly pull or rebase updates from the main branch into your active feature branch to stay up-to-date with your team's ongoing work.

Use Pull/Merge Requests: Always require code reviews via Pull Requests before merging any branch into production.

Delete After Merging: Once a branch's code is successfully merged, delete the branch locally and remotely to keep the repository clean.
## Day 4’s Question

What is the difference between git pull and git fetch? My professor advises using git pull over git fetch? Can you put your answer into a markdown format please.

## Day 5’s Question

What are alternatives to github?Please put your answer into a markdown format.

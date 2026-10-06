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

## Day 3’s Question

Explain branches in git and their best practices? Please put your answer into a markdown format.

## Day 4’s Question

What is the difference between git pull and git fetch? My professor advises using git pull over git fetch? Can you put your answer into a markdown format please.

## Day 5’s Question

What are alternatives to github?Please put your answer into a markdown format.

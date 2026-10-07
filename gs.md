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

Answer: If two developers are working on the main branch and modify the same file, the first developer can normally commit and push their changes successfully. After that push, the remote repository contains changes that the second developer does not yet have.
If the second developer tries to push without first getting those changes, Git may reject the push because the remote branch is ahead of the local branch. The second developer should use git pull to retrieve and integrate the other developer's changes.
If the developers edited different parts of the file, Git may merge the changes automatically. If they edited the same lines or overlapping sections, a merge conflict may occur. The developer must manually resolve the conflict, save the corrected file, stage it, commit the resolution, and then push again.
This is why developers should regularly use git pull when collaborating. It helps keep the local copy synchronized with the work of other developers and reduces the chance of conflicts.

## Day 2’s Question

What are best practices regarding how often to commit and push, including recommended frequency? Please put your answer into a markdown format.

Answer:Developers should commit often, usually after completing a small, logical piece of work such as a feature or bug fix. Commits should be clear and should ideally contain working code. Developers should also push regularly so teammates can access their changes. A good minimum is at least once per day when collaborating, but pushing after important completed work is even better.

## Day 3’s Question

Explain branches in git and their best practices? Please put your answer into a markdown format.

Answer: A branch in Git is a separate line of development that allows developers to work on changes without affecting the main branch. Best practices include creating a branch for each feature or fix, giving branches clear names, keeping them focused on one task, and regularly pulling changes from the main branch to stay up to date. After the work is tested and reviewed, the branch can be merged back into `main`.

## Day 4’s Question

What is the difference between git pull and git fetch? My professor advises using git pull over git fetch? Can you put your answer into a markdown format please.

Answer: 

## Day 5’s Question

What are alternatives to github?Please put your answer into a markdown format.

Answer: 

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

**Answer:**
If two coders modify the same file on the main branch, the person who pushes first will have their changes added to the remote repository. When the second coder tries to push, Git may reject the push because their local branch is behind the remote branch, and they may need to pull the new changes and resolve a merge conflict if the same lines were changed. This can cause extra work and is one reason teams often use branches when working on separate features.

## Day 2’s Question

What are best practices regarding how often to commit and push, including recommended frequency? Please put your answer into a markdown format.

**Answer:**
A good practice is to commit whenever you have completed a small, meaningful piece of work rather than waiting until an entire project is finished. There is no exact required number of commits per day, but committing several times during a work session can make it easier to track changes and undo mistakes. Pushing should also be done regularly, such as after completing a logical piece of work or at the end of a work session, so the remote repository stays reasonably up to date.


## Day 3’s Question

Explain branches in git and their best practices? Please put your answer into a markdown format.

**Answer:**
Branches in Git allow developers to work on features, fixes, or other changes without directly changing the main branch. A common best practice is to create a separate branch for each feature or task, make and test the changes there, and then merge the branch into the main branch when the work is ready. This helps keep the main branch stable and allows multiple developers to work on different parts of a project at the same time.

## Day 4’s Question

What is the difference between git pull and git fetch? My professor advises using git pull over git fetch? Can you put your answer into a markdown format please.

**Answer:**
git fetch downloads the latest changes from the remote repository but does not automatically apply those changes to your current branch. git pull downloads the changes and then integrates them into your current branch, which makes it a more convenient command when you want to update your local files. Since my professor recommends using git pull, it makes sense for this assignment because it allows me to get the latest version of the shared repository before making my edits.

## Day 5’s Question

What are alternatives to github?Please put your answer into a markdown format.

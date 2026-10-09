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

1. When two coders work on the same file, problems will happen when they update their local repository.
the first coder can commit and push there changes successfully. However, when the second coder tries to push, Git may reject the push
because the remote repository has newer changes.
2. the second coder must use 'git pull' to get the latest changes before pushing agian. If both coders try to change the same line, a merge conflict will occur.

## Day 2’s Question

What are best practices regarding how often to commit and push, including recommended frequency? Please put your answer into a markdown format.

##A good practice is to commit changes frequently instead of waiting until the entire project is finished. Developers should commit after completing a small task, fixing a bug, or making a impactful change. This makes it easier to track prrogress and identify mistakes.

## Day 3’s Question

Explain branches in git and their best practices? Please put your answer into a markdown format.

*Branches in Git allow developers to work on different parts of a project without directylu changing the main branch*

## Day 4’s Question

What is the difference between git pull and git fetch? My professor advises using git pull over git fetch? Can you put your answer into a markdown format please.

## Day 5’s Question

What are alternatives to github?Please put your answer into a markdown format.

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

### Answer - Day 1
If two coders modify the same file on the main branch, the first coder can commit and push their changes normally. When the second coder tries to push, Git may reject the push because their local branch is now behind the remote branch.
The second coder would need to **pull the newest changes** before pushing. If both coder changed the same lines of the file, this could cause a **merge conflict** that would need to be resolved before the second coder can successfully push. If they changed different parts of the file, Git may be able to merge the changes automatically.
This is why it is important to use 'git pull' regularly when multiple developers are working in the same repository.

## Day 2’s Question

What are best practices regarding how often to commit and push, including recommended frequency? Please put your answer into a markdown format.

### Answer - Day 2

A good practice is to **commit frequently**, especially after completing and testing a specific task or meaningful change. Commits should be small enough that they are easy to understand and should include a clear message explaining what was changed.

Developers should also **push regularly** so their work is available to the rest of the team and backed up in the remote repository. At minimum, pulling and pushing daily is a good habit when working with others, but commits and pushes may happen multiple times throughout the day as tasks are completed. Before pushing, changes should be tested to make sure the code is working properly.

## Day 3’s Question

Explain branches in git and their best practices? Please put your answer into a markdown format.

## Day 4’s Question

What is the difference between git pull and git fetch? My professor advises using git pull over git fetch? Can you put your answer into a markdown format please.

## Day 5’s Question

What are alternatives to github?Please put your answer into a markdown format.

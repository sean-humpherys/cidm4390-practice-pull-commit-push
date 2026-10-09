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

## Response:
If both coders start from the same version, make changes, and commit locally, both commits can succeed. The issue occurs when they push.
1. The first coder pushes successfully. Their commit updates the remote main branch.
2. The second coder’s push is usually rejected. Their local branch does not include the first coder’s commit. Git rejects the push as a non-fast-forward update to prevent overwriting that work.
3. The second coder must integrate the remote changes. They can fetch and merge or rebase before pushing again.

Possible outcomes
Changes made    
1.Different parts of the same file  
2.The same or overlapping lines 
3.Changes that merge cleanly but interact badly 
4.The second coder force-pushes
Consequence
1.Git can often combine the changes automatically.
2.A merge conflict may occur and require manual resolution.
3.The code may contain bugs even though Git reports no conflict.
4.They may overwrite remote history and remove the first coder’s commit from main.

Recommended approach: Use separate feature branches and pull requests, coordinate changes, and test the combined code before merging into main.

## Day 2’s Question

What are best practices regarding how often to commit and push, including recommended frequency? Please put your answer into a markdown format.

## Response: Commit Best Practices
- Keep commits small and focused. Each commit should represent one logical change. Separate unrelated fixes, features, and formatting changes. GitHub recommends frequent commits organized around logical units of work. git commit · GitHub
- Write descriptive messages. Use messages such as Fix login validation for empty passwords instead of Updated stuff.
- Review before committing. Check git status and git diff so you include only intended changes.
- Check that changes work. Run relevant tests before committing completed work. Clearly label unfinished checkpoints on your own working branch.
Push Best Practices
- Use feature branches and pull requests when working with others, following the team’s workflow. GitHub Docs
- Push regularly so your committed work is available remotely and teammates can review it.
- Fetch and integrate remote changes frequently. This keeps your branch closer to the shared code and helps reveal conflicts earlier. GitHub Docs
- Avoid force-pushing shared branches. Coordinate any history rewriting with affected teammates.
- Consider automated checks. A push may trigger builds and tests, so follow the project’s expectations. GitHub Docs
A useful default: commit whenever you finish a coherent change, push after a few commits, and push your progress before ending your work session.


## Day 3’s Question

Explain branches in git and their best practices? Please put your answer into a markdown format.

## Day 4’s Question

What is the difference between git pull and git fetch? My professor advises using git pull over git fetch? Can you put your answer into a markdown format please.

## Day 5’s Question

What are alternatives to github?Please put your answer into a markdown format.

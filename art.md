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

# Consequences of Two Coders Modifying the Same File on the Main Branch

If two coders modify the **same file** while working directly on the `main` branch and commit/push at different times, the result depends on whether their changes overlap.

## Scenario

1. **Coder A** modifies the file.
2. Coder A commits and pushes the changes to `main`.
3. **Coder B** modifies the same file based on an older version.
4. Coder B tries to commit and push their changes.

### If the changes do not conflict

Git may be able to automatically combine the changes.

- Coder A's changes remain.
- Coder B's changes are added.
- Both commits can exist in the `main` branch.

### If the changes conflict

If both coders changed the **same lines or nearby sections**, Git may detect a **merge conflict**.

Coder B's push may be rejected because their local branch is behind the remote `main` branch.

Coder B would then need to:

1. Pull the latest changes from `main`.
2. Resolve the merge conflict manually.
3. Commit the resolved changes.
4. Push the updated branch to `main`.

## Example

Suppose the original file contains:

```text
Hello World


## Day 2’s Question

What are best practices regarding how often to commit and push, including recommended frequency? Please put your answer into a markdown format.

## Day 3’s Question

Explain branches in git and their best practices? Please put your answer into a markdown format.

## Day 4’s Question

What is the difference between git pull and git fetch? My professor advises using git pull over git fetch? Can you put your answer into a markdown format please.

## Day 5’s Question

What are alternatives to github?Please put your answer into a markdown format.

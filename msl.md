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

# Two Coders Editing the Same File on `main`

The outcome depends on **which lines** each person changed and **who pushes first**.

## Scenario

1. Alice and Bob both start from the same commit on `main`.
2. Both edit `app.py` and commit locally.
3. Alice pushes first, and her push succeeds.
4. Bob pushes later and is **rejected** with a "non-fast-forward" error.

```text
! [rejected]  main -> main (fetch first)
```

The remote history has moved ahead of Bob's local copy, and Git will not overwrite it.

## What Bob must do

Bob has to integrate Alice's work before he can push:

```bash
git pull --rebase origin main   # or: git pull (merge)
```

There are two possible results:

| Situation | Result |
|---|---|
| Different parts of the file | Git **auto-merges**. No conflict, and Bob pushes normally. |
| Same lines changed | **Merge conflict**. Bob must resolve it by hand. |

## Resolving a conflict

Git marks the file like this:

```text
<<<<<<< HEAD
Alice's version
=======
Bob's version
>>>>>>> bob-commit
```

Bob then:

1. Edits the file to keep the correct combined code.
2. Removes the conflict markers.
3. Runs `git add app.py`.
4. Continues with `git rebase --continue` (or `git commit` for a merge).
5. Runs `git push origin main`.

## Consequences

- **No lost work.** Git blocks the push rather than silently overwriting Alice's commits.
- **Delay.** Bob has to stop and reconcile before pushing.
- **Risk of semantic bugs.** A clean auto-merge can still break the logic, for example when two people change related functions. Tests should be run after merging.
- **History shape.** Merging creates a merge commit. Rebasing keeps history linear but rewrites Bob's local commits.
- **Danger of force-pushing.** `git push --force` would erase Alice's commits from the remote. Avoid it on shared branches.

## Best practices

- Pull often, and before starting new work.
- Use feature branches and pull requests instead of committing straight to `main`.
- Protect `main` with branch rules and required reviews.
- Run CI tests on every push.
- Keep commits small and communicate about who is editing which files.

Is your team committing straight to `main` or considering a branching workflow? Tell me which, and I'll write a step-by-step workflow with branch naming, PR rules and protection settings tailored to your team.


## Day 2’s Question

What are best practices regarding how often to commit and push, including recommended frequency? Please put your answer into a markdown format.

## Day 3’s Question

Explain branches in git and their best practices? Please put your answer into a markdown format.

## Day 4’s Question

What is the difference between git pull and git fetch? My professor advises using git pull over git fetch? Can you put your answer into a markdown format please.

## Day 5’s Question

What are alternatives to github?Please put your answer into a markdown format.

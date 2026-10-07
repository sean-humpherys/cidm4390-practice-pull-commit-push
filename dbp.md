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

# Two coders, one file, same branch

If two coders, working on the `main` branch, modify the same file, commit, and push at different times, the second push is rejected. Git will not overwrite commits that are already on `main`.

## What actually happens

Both coders start from the same commit on `main` and edit the same file.

1. Coder A commits and pushes. That succeeds. Remote `main` now has A's commit.
2. Coder B commits locally. Their commit is still based on the old tip of `main`, so their history has diverged from the remote.
3. Coder B pushes. Git refuses it because it is not a fast-forward. Typical message:

```text
! [rejected] main -> main (fetch first)
error: failed to push some refs
hint: Updates were rejected because the remote contains work that you do not have locally.
```

Nothing on the remote is lost or overwritten. B's commit stays only on their machine until they integrate A's work.

## What B has to do

```bash
git pull origin main
# or: git fetch origin && git merge origin/main
# or: git pull --rebase origin main
```

Then one of two things happens:

- **Different lines were changed.** Git auto-merges, B commits the merge (or the rebase finishes), and the next push succeeds.
- **The same lines were changed.** Git stops with a merge conflict. The file contains conflict markers:

```text
<<<<<<< HEAD
B's version
=======
A's version
>>>>>>> origin/main
```

B edits the file to the intended result, removes the markers, then:

```bash
git add <file>
git commit          # merge case
# or: git rebase --continue
git push origin main
```

## Consequences

- The later push never silently replaces the earlier one. That is what protects `main`.
- History on `main` becomes non-linear if they merge (a merge commit with two parents), or stays linear if they rebase.
- Whoever pushes second owns the conflict resolution. A bad resolution can drop the other person's change even though the push itself was safe.
- Working directly on `main` makes this routine. Separate branches and a pull request avoid the race: each person pushes their own branch, and GitHub only merges when the branch is up to date with `main`.

## Day 2’s Question

What are best practices regarding how often to commit and push, including recommended frequency? Please put your answer into a markdown format.

## Day 3’s Question

Explain branches in git and their best practices? Please put your answer into a markdown format.

## Day 4’s Question

What is the difference between git pull and git fetch? My professor advises using git pull over git fetch? Can you put your answer into a markdown format please.

## Day 5’s Question

What are alternatives to github?Please put your answer into a markdown format.

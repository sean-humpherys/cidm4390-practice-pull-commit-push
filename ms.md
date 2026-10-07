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

## Scenario
Coder A commits and pushes to `main` first. Coder B committed locally on the same file, based on the older version of `main`, and pushes afterward.

## Consequences

**1. B's push is rejected**
Git refuses it as a non-fast-forward push, because the remote has commits B's local branch lacks. Nothing on the remote changes.

```
! [rejected]  main -> main (fetch first)
```

**2. B must integrate A's work first**
B runs `git pull` (fetch + merge) or `git pull --rebase` (fetch + replay B's commits on top of A's).

**3. Result depends on what each person changed**

| Situation | Outcome |
|---|---|
| Different regions of the file | Git auto-merges. With merge, a merge commit is created. With rebase, history stays linear. |
| Same lines changed | Merge conflict. Git marks the file with `<<<<<<<`, `=======`, `>>>>>>>`. B must resolve it by hand, stage the file, and finish the merge or rebase (`git commit` or `git rebase --continue`). |
| Clean merge but incompatible logic (e.g., A renames a function, B adds a call to the old name) | No Git warning. The code can break at build or runtime. Only tests or CI catch it. |

**4. Force push (`git push --force`) is the dangerous case**
If B forces the push instead of integrating, A's commits are dropped from the remote `main`. They can be recovered from A's local clone or the reflog, but anyone who pulls next gets a history without them. `--force-with-lease` fails if the remote has moved, which avoids this.

**5. Rebase side effect**
`git pull --rebase` rewrites B's local commits (new hashes). This is harmless if they haven't been pushed.

**6. No consequence if the timing differs**
If B pulled A's commit before committing, the push is a plain fast-forward with no conflict, regardless of both editing the same file.

## Prevention
- Pull or rebase frequently before starting work and before pushing.
- Use feature branches with pull requests instead of committing directly to `main`.
- Enable branch protection (block force pushes, require review and passing CI).
- Keep commits small and files focused to reduce overlap.


## Day 2’s Question

What are best practices regarding how often to commit and push, including recommended frequency? Please put your answer into a markdown format.

## Best Practices
Commit often

    After each small, logical change

    When tests pass

    At least once per hour

Push regularly

    Every 1–3 commits

    At least once per day

    After finishing a sub-feature or before stopping work

Keep commits atomic

    One logical change per commit

    Clear message

    Easy to review and revert

Simple rule: Commit small and often. Push every few commits or daily.


## Day 3’s Question

Explain branches in git and their best practices? Please put your answer into a markdown format.

## Branches

A branch is a lightweight pointer to a commit, not a copy of files. HEAD points to the branch you have checked out, and each new commit moves that branch forward.

Core commands
bash
git branch -vv                  # list branches with upstream info
git switch -c feature/login     # create and switch (Git 2.23+)
git merge feature/login         # merge into current branch
git rebase main                 # replay current branch on top of main
git branch -d feature/login     # delete if merged
git push origin --delete feature/login   # delete remote branch
git fetch --prune               # clear stale remote-tracking refs
Merge vs. rebase
Merge: preserves history, non-destructive. Use for integrating into shared branches.
Rebase: rewrites commits into linear history. Use only on your own unshared branches.
Squash merge: collapses a branch into one commit. Clean history, loses individual commits.

Strategies
Trunk-based: very short-lived branches merged into main often. Suits continuous deployment.
GitHub Flow: main always deployable; branch, pull request, review, merge.
Git Flow: long-lived main and develop plus feature/*, release/*, hotfix/*. Suits versioned releases, heavier process.

Best practices
Name consistently: feature/user-login, fix/checkout-null, optionally with a ticket ID.
Keep branches short-lived and single-purpose.
Branch from an up-to-date base and sync with it regularly.
Delete branches after merging, locally and remotely.
Protect main: require pull requests, passing CI, and review; block force pushes.
Never rewrite commits others have pulled. If you must force push, use --force-with-lease.
Recover deleted branches with git reflog.

## Day 4’s Question

What is the difference between git pull and git fetch? My professor advises using git pull over git fetch? Can you put your answer into a markdown format please.

## Day 5’s Question

What are alternatives to github?Please put your answer into a markdown format.

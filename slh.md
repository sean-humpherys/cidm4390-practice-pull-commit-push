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

Developer A and Developer B both clone or pull the `main` branch at the same point. Each edits the same file, commits locally, and pushes to the shared remote (for example, GitHub) at a different time.

## What Happens

### 1. The first push succeeds

Developer A pushes first. The remote `main` branch now has a commit that Developer B does not have locally.

### 2. The second push is rejected

When Developer B tries to push, Git refuses with a message similar to:

```
! [rejected]        main -> main (fetch first)
error: failed to push some refs
hint: Updates were rejected because the remote contains work that you do not have locally.
```

Git does not let B overwrite A's work silently. B's local history and the remote history have **diverged**.

### 3. Developer B must integrate A's changes first

B runs one of the following:

```bash
git pull            # fetch + merge (creates a merge commit)
git pull --rebase   # fetch + replay B's commit on top of A's
```

Then one of two outcomes occurs.

| Situation | Result |
|---|---|
| A and B changed **different, non-overlapping lines** | Git merges automatically. B pushes successfully. |
| A and B changed the **same or adjacent lines** | Git reports a **merge conflict**. B must resolve it manually. |

### 4. Resolving a merge conflict

Git marks the conflicting section in the file:

```
<<<<<<< HEAD
B's version of the line
=======
A's version of the line
>>>>>>> origin/main
```

B must:

1. Edit the file to keep the correct combined result and remove the markers.
2. Stage the file: `git add <file>`
3. Finish the merge (`git commit`) or rebase (`git rebase --continue`).
4. Push: `git push`

## Risks and Consequences

- **Lost work from force pushing.** If B runs `git push --force` instead of pulling, A's commit is overwritten on the remote. This is the most serious consequence.
- **Incorrect conflict resolution.** B may accidentally delete or garble A's changes while resolving the conflict.
- **Semantic conflicts.** Git may merge cleanly at the text level, yet the combined code fails (for example, A renames a function while B adds a new call to the old name). Tests or a build are needed to catch this.
- **Messy history.** Repeated `git pull` merges on `main` create extra merge commits that make history harder to read.
- **Broken `main` branch.** Unreviewed direct commits mean errors reach the shared branch immediately and affect everyone.

## Best Practices to Avoid These Problems

1. **Use feature branches** instead of committing directly to `main`.
2. **Merge through pull requests** so changes are reviewed and conflicts are resolved before reaching `main`.
3. **Enable branch protection** on `main` to block direct pushes and force pushes.
4. **Pull frequently** (`git pull --rebase`) to stay current and keep conflicts small.
5. **Commit small, focused changes** to reduce overlap between developers.
6. **Communicate** when two people need to work on the same file.
7. **Run automated tests** (CI) on every pull request to catch semantic conflicts.
8. **Never force push to a shared branch** unless the whole team agrees.

## Summary

Git protects the first developer's work by rejecting the second push. The second developer must pull, merge or rebase, and resolve any conflicts before pushing. The real dangers are force pushing, careless conflict resolution, and code that merges cleanly but no longer works. Feature branches, pull requests, and branch protection prevent most of these issues.


## Day 2’s Question

What are best practices regarding how often to commit and push, including recommended frequency? Please put your answer into a markdown format.

## Day 3’s Question

Explain branches in git and their best practices? Please put your answer into a markdown format.

## Day 4’s Question

What is the difference between git pull and git fetch? My professor advises using git pull over git fetch? Can you put your answer into a markdown format please.

## Day 5’s Question

What are alternatives to github?Please put your answer into a markdown format.

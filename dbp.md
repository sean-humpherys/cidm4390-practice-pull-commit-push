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

# Git Best Practices: How Often Should You Commit and Push?

## 1. How Often Should You Commit?

A **commit** saves a snapshot of changes in your local Git repository.

**Best practice:** Commit frequently, whenever you complete a small, meaningful unit of work.

- Commit after completing a feature, fixing a bug, or making a logical improvement.
- Make small, focused commits rather than one large commit containing many unrelated changes.
- Write clear, descriptive commit messages explaining what changed.
- Commit several times a day when actively developing, if meaningful changes are completed.
- Test your changes before committing whenever practical.

**Example:**

```bash
git add -A
git commit -m "Add login form validation"
```

## 2. How Often Should You Push?

A **push** uploads your local commits to a remote repository, such as GitHub.

**Best practice:** Push regularly, especially after completing and testing meaningful work.

- Push after finishing a logical unit of work that is ready to share.
- Push at least once per working day when actively collaborating, if you have commits to share.
- Push before switching computers or ending your work session.
- Push more frequently when teammates depend on your changes.
- Avoid pushing broken or untested code to shared branches.

**Example:**

```bash
git push
```

## 3. What Is the Difference Between Commit and Push?

| Commit | Push |
|---|---|
| Saves changes locally | Sends commits to the remote repository |
| Creates a record of changes | Shares changes with collaborators |
| Can be done without internet access | Requires access to the remote repository |
| Should happen after meaningful changes | Should happen when changes are ready to share |

## 4. Recommended Daily Git Workflow

1. **Pull** the latest changes before starting work.
2. Make a small, meaningful change.
3. **Test** or review the change.
4. **Commit** the completed change with a descriptive message.
5. **Push** the commit to the remote repository.
6. Run `git status` to verify your repository's state.

```bash
git pull
git add -A
git commit -m "Describe the completed change"
git push
git status
```

## 5. Key Takeaway

**Commit often, push regularly, and pull before starting work.**

There is no universal rule requiring a commit every certain number of minutes. The frequency should depend on meaningful progress, the team's workflow, and how frequently changes need to be shared.


## Day 3’s Question

Explain branches in git and their best practices? Please put your answer into a markdown format.

# Git Branches and Best Practices

## 1. What Is a Git Branch?

A Git branch is an independent line of development that allows developers to work on changes without immediately affecting the main branch. Branches help teams develop features, fix bugs, and experiment safely.

## 2. Why Are Branches Important?

- **Parallel development:** Multiple developers can work on different features simultaneously.
- **Isolation:** Unfinished changes remain separate from stable code.
- **Collaboration:** Changes can be reviewed before being merged.
- **Experimentation:** Developers can test ideas without disrupting the main branch.

## 3. Common Git Branch Commands

| Command | Purpose |
|---|---|
| `git branch` | List local branches. |
| `git switch -c feature-login` | Create and switch to a new branch. |
| `git switch main` | Switch back to the main branch. |
| `git merge feature-login` | Merge the feature branch into the current branch. |
| `git branch -d feature-login` | Delete a merged local branch. |
| `git push -u origin feature-login` | Publish a new branch to the remote repository. |

## 4. Best Practices for Git Branches

1. **Keep the main branch stable.** Develop and test changes before merging them into `main`.
2. **Use descriptive branch names.** Examples: `feature/login`, `bugfix/payment-error`, and `docs/readme-update`.
3. **Create focused branches.** Each branch should address one feature, bug, or specific task.
4. **Keep branches short-lived.** Merge completed work regularly to reduce conflicts.
5. **Stay synchronized.** Fetch or pull updates and integrate relevant changes from `main` into your working branch when necessary.
6. **Commit meaningful changes.** Use small commits with clear messages.
7. **Review and test before merging.** Use pull requests when the team workflow requires them.
8. **Resolve merge conflicts carefully.** Review conflicting changes and test the result.
9. **Delete merged branches.** Remove branches that are no longer needed to keep the repository organized.

## 5. Example Branching Workflow

```bash
git switch main
git pull
git switch -c feature-login
# Edit and test the login feature
git add -A
git commit -m "Add login feature"
git push -u origin feature-login
```

After the feature is reviewed, it can be merged into `main` through a pull request.

## 6. Key Takeaway

Git branches allow developers to work independently while protecting stable code. The most important practices are to create focused branches, use descriptive names, synchronize regularly, test changes, review before merging, and remove branches after merging.

## Day 4’s Question

What is the difference between git pull and git fetch? My professor advises using git pull over git fetch? Can you put your answer into a markdown format please.

## Day 5’s Question

What are alternatives to github?Please put your answer into a markdown format.

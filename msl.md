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

# Git Best Practices: How Often Should You Commit and Push?

The general best practice is to commit small, logical changes frequently and push your work regularly. This makes collaboration easier, reduces the risk of losing work, and simplifies troubleshooting when something breaks.

## 1. Recommended Frequency

| Action                     | Recommended frequency                                                        | Purpose                                                 |
| -------------------------- | ---------------------------------------------------------------------------- | ------------------------------------------------------- |
| Commit                     | Every 15–60 minutes of active work, or whenever a logical change is complete | Save a meaningful, recoverable unit of work             |
| Push                       | Every 30–60 minutes, or after completing a meaningful task                   | Share your changes with the remote repository           |
| Pull / sync                | Before starting work and periodically throughout the day                     | Incorporate teammates' changes and reduce conflicts     |
| Merge / integrate          | Frequently, ideally several times a day for active shared branches           | Keep code integrated and detect problems early          |
| Create a pull request (PR) | When a feature or logical task is ready for review                           | Enable code review, testing, and controlled integration |

These time intervals are practical guidelines, not rigid rules. The best frequency depends on task size, team workflow, and repository policies.

## 2. When Should You Commit?

A commit should represent a small, logical unit of work that you can understand later.

Good times to commit:

- You finish implementing a specific function.
- You fix a bug and verify the fix.
- You complete a small portion of a feature.
- You update tests or documentation related to a completed change.
- You reach a stable checkpoint before attempting a risky modification.

Avoid committing:

- Every single keystroke or trivial edit.
- Large collections of unrelated changes.
- Code that is knowingly broken, unless your team explicitly uses work-in-progress commits.
- Passwords, API keys, credentials, or other sensitive information.

### Example

Suppose you are developing a login feature.

Commit 1: Create login form

The form is implemented and its basic validation works.

Commit 2: Add authentication logic

The authentication process is implemented as a separate, understandable change.

Commit 3: Add login error handling

Invalid credentials and authentication failures are handled appropriately.

This is preferable to one enormous commit titled `Finished login feature` because each step can be reviewed and troubleshot independently.

## 3. When Should You Push?

A commit saves a snapshot in your local repository. A push sends your committed changes to a remote repository, such as GitHub, GitLab, or Bitbucket.

Push when:

- You have completed a meaningful piece of work.
- You want your teammates to access your latest changes.
- You want a backup of your local commits on the remote server.
- You are ready to request feedback or open a pull request.
- You are about to stop working for the day.

Recommended rule: Push at least a few times throughout a normal working day rather than keeping all your commits local until the end of the day.

One important distinction: pushing to a shared branch does not automatically mean your changes have been reviewed, tested, or merged into the production code.

## 4. A Practical Daily Workflow

Here is a workflow suitable for a team of two developers or a small development team.

Step 1 — Start your workday

Pull the latest changes from the remote branch and check the status of your local repository.

Step 2 — Work on a task

Implement a focused change and run relevant tests.

Step 3 — Commit the change

Create a descriptive commit once you reach a coherent checkpoint.

Step 4 — Push to the remote

Push your branch after a meaningful task or roughly every 30–60 minutes of active work.

Step 5 — Review and integrate

Open a pull request when the task is ready, address feedback, and integrate it according to your team's workflow.

## 5. What If Two Developers Edit the Same File?

Since multiple developers can work on the same file, commit and push frequency becomes especially important.

Consider this scenario:

1. Developer A and Developer B both pull the latest version of `app.py`.
2. Both modify the same file in different ways.
3. Developer A commits and pushes first.
4. Developer B tries to push their changes.

Git will generally reject Developer B's push if it cannot be applied as a fast-forward update. This protects the remote branch from silently losing Developer A's changes.

Developer B should then fetch or pull the latest changes, integrate them with their own work, resolve any merge conflicts, run tests, and push again.

Best practices for this situation:

- Push changes regularly so teammates can see your progress.
- Communicate when you are modifying the same file or feature.
- Use feature branches rather than having everyone work directly on `main`.
- Keep pull requests focused and reasonably small.
- Integrate changes frequently to catch conflicts before they become complicated.

Important: Frequent commits help you manage your own work, but only pushing makes those commits available on the remote repository. Neither action alone prevents merge conflicts.

## 6. Recommended Git Commands

A typical sequence might look like this:

```
# Check your current changes
git status

# Review the changes
git diff

# Stage the specific files you intend to commit
git add app.py

# Commit a logical unit of work
git commit -m "Add login form validation"

# Push your branch to the remote repository
git push
```

When you need to incorporate teammates' changes, a common approach is:

```
# Download information about remote changes
git fetch origin

# Integrate changes from the remote branch
git pull --rebase
```

Use the appropriate remote and branch for your project. `git pull --rebase` replays your local commits on top of the updated upstream history; it may require conflict resolution. Teams that use merge-based workflows may prefer a regular `git pull` instead. Avoid rebasing commits that teammates are already relying on unless your team agrees on that workflow.

## 7. Common Mistakes to Avoid

| Mistake                                      | Why it is a problem                                | Better practice                                                                          |
| -------------------------------------------- | -------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| Waiting until the end of the day to commit   | Makes recovery and troubleshooting harder          | Commit at logical checkpoints                                                            |
| Committing but rarely pushing                | Leaves your latest work only on your machine       | Push regularly                                                                           |
| Making one huge commit                       | Makes review and debugging harder                  | Break work into logical changes                                                          |
| Pushing untested changes to `main`           | Can disrupt other developers                       | Use branches and automated checks                                                        |
| Editing the same files without communicating | Increases conflict risk                            | Coordinate and integrate frequently                                                      |
| Using `git push --force` casually            | Can overwrite remote history and disrupt teammates | Prefer normal pushes; use safer force-push options only when appropriate and coordinated |

## Final Recommendation

For a small development team, I recommend starting with this routine:

- Commit: Whenever you complete a logical, testable unit of work—often every 15–60 minutes.
- Push: Every 30–60 minutes, after meaningful milestones, and before finishing for the day.
- Pull or fetch: At the start of the day and whenever you need to incorporate teammates' changes.
- Integrate: Several times a day when practical, using branches and pull requests where appropriate.
- Protect `main`: Require review and automated tests for changes entering the main branch.

The most important principle is to commit based on meaningful changes, not a stopwatch, and push frequently enough that your work is shared and recoverable.

## Day 3’s Question

Explain branches in git and their best practices? Please put your answer into a markdown format.

## Day 4’s Question

What is the difference between git pull and git fetch? My professor advises using git pull over git fetch? Can you put your answer into a markdown format please.

## Day 5’s Question

What are alternatives to github?Please put your answer into a markdown format.

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

# Git Branches: Explanation and Best Practices

## 1. What Is a Branch in Git?

A **branch in Git is an independent line of development** that allows you to work on a feature, bug fix, or experiment without immediately affecting the main codebase.

Think of your project as a book. The `main` branch is the official version, while a branch lets you write and revise a separate chapter before incorporating it into the final book.

Branches are lightweight in Git, so creating and switching between them is fast and inexpensive.

### Example

Suppose you are building a website and want to add a login system.

Your repository might look like this:

```
main
 |
 A --- B --- C
              \
               D --- E  (feature/login)
```

- `main`: The primary, stable version of your project.
- `A`, `B`, `C`: Existing commits.
- `feature/login`: A separate branch where you develop the login system.
- `D`, `E`: Commits containing your login-related changes.

You can work on the login system without immediately introducing unfinished code into `main`.

Once the feature is ready and reviewed, you can merge it into `main`.

---

## 2. Common Types of Git Branches

Different teams use different branching strategies, but these are the most common branch types.

### A. Main Branch (`main`)

The `main` branch is generally the primary branch of a project.

**Best practices:**

- Keep the code functional and reasonably stable.
- Require code reviews before merging changes in team projects.
- Run automated tests before merging.
- Avoid directly committing experimental or unfinished code.
- Protect the branch against accidental deletion or unauthorized changes.

Some teams deploy directly from `main`, so they aim to keep it consistently ready for release.

### B. Feature Branches

Feature branches are used to develop new functionality independently.

Example names:

```
feature/user-login
feature/payment-system
feature/search-functionality
```

**Best practices:**

- Create a new branch for each distinct feature.
- Keep branches focused on one task.
- Commit changes regularly.
- Synchronize with `main` when appropriate.
- Merge the feature when it is tested and reviewed.
- Delete the branch after merging if it is no longer needed.

**Example workflow:**

```
git switch main
git pull origin main
git switch -c feature/user-login
```

Make your changes, then commit them:

```
git add .
git commit -m "Add user login functionality"
```

When the feature is ready, push it:

```
git push -u origin feature/user-login
```

You can then open a pull request to merge it into `main`.

### C. Bug-Fix Branches

Bug-fix branches isolate work to correct an existing problem.

Example names:

```
fix/login-validation
fix/navbar-layout
fix/database-connection
```

**Best practices:**

- Describe the bug clearly in the branch name.
- Make the smallest reasonable change that fixes the problem.
- Add or update tests to prevent the bug from returning.
- Avoid mixing unrelated improvements into the same branch.

### D. Release Branches

Some teams create release branches when preparing a specific version of a product.

Example:

```
release/2.0
```

A release branch can be used for final testing, documentation, and release-specific bug fixes while other development continues.

**Best practices:**

- Use release branches only when your release process benefits from them.
- Keep last-minute changes limited to release preparation and necessary fixes.
- Ensure critical fixes are also incorporated into the ongoing development branch.

Small teams that deploy continuously may not need release branches.

### E. Hotfix Branches

Hotfix branches are used to address urgent problems in production.

Example:

```
hotfix/payment-failure
```

Suppose your website stops processing payments. A hotfix branch allows you to correct the issue without waiting for a larger feature to be completed.

**Best practices:**

- Prioritize the immediate production issue.
- Test the fix as thoroughly as the circumstances permit.
- Review and deploy the fix promptly.
- Ensure the fix reaches other relevant branches so the bug does not reappear.

---

## 3. How Branches Work with Commits, Pushes, and Merges

Understanding these four concepts is essential.

| Concept           | Meaning                                                                        |
| ----------------- | ------------------------------------------------------------------------------ |
| Branch            | An independent line of development.                                            |
| Commit            | A saved snapshot of changes in your repository's history.                      |
| Push              | Sends local commits to a remote repository, such as GitHub.                    |
| Merge             | Integrates changes from one branch into another.                               |
| Pull              | Typically fetches remote changes and integrates them into your current branch. |
| Pull request (PR) | A platform-based proposal to review and merge changes.                         |

A branch does not automatically share your changes with teammates. You generally need to commit and push your work before they can access those commits through the remote repository.

### Local branches versus remote branches

A **local branch** exists in your local repository.

A **remote-tracking branch**, such as `origin/main`, records your local view of the remote branch.

A **remote branch** exists on the shared server, such as GitHub.

For example:

```
git branch
```

Lists local branches.

```
git branch -a
```

Lists local branches and remote-tracking branches.

```
git push origin feature/login
```

Pushes your local branch to the remote repository.

---

## 4. Recommended Branching Workflow for a Small Team

For most small teams, a straightforward approach is to keep `main` stable and use short-lived feature branches.

```
                  feature/login
                 /              \
main ----------- A                D
                                  |
main ---------------------------- M
                                  |
                              Merge to main
```

The general workflow is:

1. **Update `main`.** Retrieve the latest shared changes.
2. **Create a branch.** Give it a clear name describing your task.
3. **Make changes.** Work on the feature without modifying `main` directly.
4. **Commit frequently.** Save logical units of work with meaningful messages.
5. **Push regularly.** Back up your work and share it with teammates.
6. **Open a pull request.** Request review and automated testing.
7. **Resolve issues.** Address review feedback and any merge conflicts.
8. **Merge into `main`.** Use the team's agreed merge strategy.
9. **Delete the feature branch.** Clean up after merging.

Example commands:

```
# Update the main branch
git switch main
git pull origin main

# Create a new feature branch
git switch -c feature/shipment-tracking

# Make changes and commit them
git add .
git commit -m "Add shipment tracking page"

# Push the branch to GitHub
git push -u origin feature/shipment-tracking
```

After review and approval, merge through your team's pull request process.

Once merged, clean up:

```
git switch main
git pull origin main
git branch -d feature/shipment-tracking
```

If the remote branch has not already been deleted by your hosting platform, you can remove it with:

```
git push origin --delete feature/shipment-tracking
```

**Important:** Only delete a branch after confirming that its work has been merged or is otherwise safely preserved.

---

## 5. Best Practices for Managing Branches

### 1. Keep branches short-lived

Avoid letting feature branches sit unmerged for weeks or months.

The longer a branch exists independently, the more likely the main codebase will change in ways that conflict with it.

**Recommendation:** Aim to merge small features within a day or a few days when practical. Larger projects may require longer, but break the work into smaller, independently mergeable changes whenever possible.

### 2. Use descriptive branch names

Good branch names make it easier to understand what everyone is working on.

| Good                          | Avoid     |
| ----------------------------- | --------- |
| `feature/user-authentication` | `branch1` |
| `fix/shipment-calculation`    | `fix`     |
| `docs/api-guide`              | `stuff`   |
| `hotfix/payment-timeout`      | `urgent`  |

A common naming convention is:

```
type/short-description
```

Typical types include `feature`, `fix`, `hotfix`, `docs`, and `refactor`.

If your team uses issue tracking, you can include a ticket number:

```
feature/123-shipment-tracking
```

Agree on one naming convention and use it consistently.

### 3. Avoid direct commits to `main`

For collaborative projects, use feature branches and pull requests.

This helps prevent:

- Accidental introduction of unfinished code.
- Unreviewed changes affecting teammates.
- Broken builds and deployments.
- Difficulty identifying who introduced a problem.

For a personal project, committing directly to `main` can be perfectly reasonable. The benefit of branches increases as project complexity and collaboration increase.

### 4. Commit small, meaningful changes

A branch should contain a logical set of changes, and each commit should explain one meaningful step.

For example:

```
Add shipment tracking model
Add shipment tracking API endpoint
Add shipment tracking page
```

This is generally easier to review and troubleshoot than one enormous commit titled `Update everything`.

### 5. Keep your branch synchronized with `main`

Other developers may merge changes while you work.

Periodically integrate the latest changes from `main` into your feature branch. One common method is merging:

```
git switch main
git pull origin main
git switch feature/shipment-tracking
git merge main
```

Alternatively, you can rebase your feature branch onto the updated `main`:

```
git switch feature/shipment-tracking
git fetch origin
git rebase origin/main
```

**Which should you choose?**

- **Merge:** Preserves the existing branch history and is generally straightforward for shared branches.
- **Rebase:** Replays your commits on top of a newer base, producing a more linear history.

Avoid rebasing commits that other developers already rely on unless your team has agreed on how to handle it. Rebasing changes commit identities and may require a coordinated push.

### 6. Use pull requests and code reviews

A pull request is a chance to inspect the changes before they enter the main codebase.

A useful review checks:

- Does the code solve the intended problem?
- Are there bugs or security issues?
- Are relevant tests included and passing?
- Does the change introduce unnecessary complexity?
- Is documentation updated where needed?

For a small team, even one thoughtful review can help significantly.

### 7. Delete merged branches

Once a feature branch has been merged, delete it if it is no longer needed.

This keeps the branch list manageable and makes active work easier to identify.

Deleting a merged branch does not normally delete the commits already incorporated into `main`.

### 8. Protect important branches

For a shared project hosted on GitHub or a similar service, consider requiring:

- Pull requests before merging.
- Successful automated tests.
- Required approvals.
- Restrictions on force-pushing and branch deletion.

Branch protection is particularly useful when multiple developers share a repository.

### 9. Test before merging

Do not assume that code working on a feature branch means it will work correctly after integration.

Run relevant tests on the combined changes, ideally using continuous integration (CI).

Tests may include:

- Unit tests.
- Integration tests.
- End-to-end tests.
- Security and dependency checks.
- Build and deployment checks.

### 10. Avoid creating unnecessary branches

Branches are cheap, but managing many overlapping branches creates administrative overhead.

Create branches for meaningful, independently manageable work rather than every tiny edit.

---

## 6. What Happens When Two Developers Work on Different Branches?

Imagine two developers working on the same application.

- Developer A creates `feature/login`.
- Developer B creates `feature/shipment-tracking`.
- Both branches begin from the same version of `main`.

They can work independently, commit, and push without immediately overwriting one another's branch.

When their work is merged, Git integrates the changes. If both developers modified different parts of the code, Git can often combine the changes automatically.

However, if they modified overlapping lines in the same file, a **merge conflict** may occur. Git will require someone to resolve the conflict before completing the merge.

For example:

```
main
 |
 +--- feature/login
 |
 +--- feature/shipment-tracking
```

This is one of the primary reasons to use branches: developers can work independently, while the team integrates their changes in a controlled way.

**Important distinction:** Branches reduce the risk of disrupting each other's work, but they do not eliminate merge conflicts or guarantee that independently developed features will work together.

---

## 7. Common Branching Mistakes to Avoid

| Mistake                                       | Why it is a problem                      | Better approach                              |
| --------------------------------------------- | ---------------------------------------- | -------------------------------------------- |
| Working directly on `main` in a team          | Unreviewed changes can affect everyone.  | Use feature branches and PRs.                |
| Keeping branches open too long                | Integration becomes harder.              | Merge small changes frequently.              |
| Naming branches vaguely                       | Teammates cannot identify their purpose. | Use descriptive names.                       |
| Pushing unfinished work directly to `main`    | Can break shared code or deployments.    | Push to a feature branch.                    |
| Ignoring new commits on `main`                | Increases integration risk.              | Synchronize regularly.                       |
| Rebasing shared branches without coordination | Can disrupt collaborators' history.      | Rebase private branches or coordinate first. |
| Deleting a branch before preserving its work  | Changes may become difficult to recover. | Verify the merge first.                      |
| Using branches without testing                | Integration can introduce bugs.          | Run tests and CI before merging.             |

---

## 8. Which Branching Strategy Should You Use?

Three common approaches are worth knowing.

### Option A: Main + Short-Lived Feature Branches

**Best for:** Small teams, student projects, web applications, and teams that deploy frequently.

```
main
 ├── feature/login
 ├── feature/shipping
 └── fix/navigation
```

Developers create branches, open pull requests, and merge them into `main`.

**Advantages:**

- Simple to understand.
- Easy to maintain.
- Encourages frequent integration.
- Works well with automated testing.

**Disadvantages:**

- Requires discipline to keep `main` stable.
- Teams must coordinate when changes depend on one another.

**Recommendation:** This is the best default for most small collaborative projects.

### Option B: Git Flow

Git Flow uses several long-lived branch types, typically including:

```
main
develop
feature/*
release/*
hotfix/*
```

Features are generally integrated into `develop`, while releases and urgent fixes follow separate paths.

**Best for:** Projects with scheduled releases, multiple supported versions, or formal release-management requirements.

**Advantages:**

- Separates ongoing development from production releases.
- Provides a structured release process.

**Disadvantages:**

- More complex.
- Creates additional integration and maintenance work.
- Often unnecessary for teams deploying continuously.

### Option C: Trunk-Based Development

Trunk-based development centers on a shared mainline, with developers integrating changes very frequently. Feature branches, when used, are kept very short-lived.

**Best for:** Teams with strong automated testing, continuous integration, and frequent deployments.

**Advantages:**

- Reduces long-running divergence.
- Encourages rapid integration.
- Supports frequent releases.

**Disadvantages:**

- Requires good testing and integration practices.
- Incomplete features may need feature flags or other techniques to remain hidden from users.

---

## 9. A Practical Set of Rules for Your Team

If you are starting a collaborative Git project, these rules provide a strong foundation:

1. Keep `main` stable.
2. Create one branch per feature, bug fix, or clearly defined task.
3. Use consistent names, such as `feature/...` and `fix/...`.
4. Commit whenever you complete a meaningful unit of work.
5. Push regularly to back up your work and share progress.
6. Update your branch with recent changes from `main`.
7. Use pull requests for review before merging.
8. Require relevant tests to pass before merging.
9. Avoid force-pushing shared branches without coordination.
10. Delete branches after confirming their work has been merged.

### Final takeaway

**Use branches to isolate work, commits to record progress, pushes to share work, and pull requests to review and integrate changes.**

For most small teams, `main` plus short-lived feature branches is a practical balance between simplicity, collaboration, and code quality.

Clarify pull versus fetch behaviorAdd a merge-conflict resolution walkthrough

## Day 4’s Question

# Git Pull vs. Git Fetch: What's the Difference?

The main difference is that `git fetch` downloads changes from a remote repository without integrating them into your current branch, while `git pull` downloads changes and integrates them into your current branch.

Both commands help you keep your local repository up to date with a remote repository, such as GitHub.

## 1. How `git fetch` works

The `git fetch` command retrieves new commits and other updates from a remote repository, but does not automatically merge those changes into your current working branch.

For example:

```
git fetch origin
```

Here is what happens:

1. Git contacts the remote repository named `origin`.
2. Git downloads new commits and updates its remote-tracking references.
3. Your current branch and working files remain unchanged.
4. You can inspect the incoming changes before deciding whether to integrate them.

### Example

Suppose your local `main` branch has this history:

Your local main branch

`A` → `B` → `C`

Remote origin/main has additional commits

`A` → `B` → `C` →&#x20;

&#x20;`D` → `E`

After running `git fetch origin`, Git downloads commits `D` and `E`, but your local `main` branch still points to `C`.

You can examine the difference before integrating the updates:

```
git log main..origin/main --oneline
```

This shows commits that are in `origin/main` but not yet in your local `main`.

When should you use `git fetch`?

- You want to inspect incoming changes before integrating them.
- You are collaborating on a project and want to see what other developers have done.
- You want more control over when and how changes enter your current branch.
- You want to check for remote updates without changing your working files.

## 2. How `git pull` works

The `git pull` command fetches remote changes and then integrates them into your current branch.

For example:

```
git pull origin main
```

Conceptually, this performs two operations:

1. Fetches updates from the remote `main` branch.
2. Integrates those updates into your current branch, usually by merging or rebasing, depending on your Git configuration and command options.

With the default merge behavior, if your local branch has no new commits of its own, Git can often perform a fast-forward update.

Using the previous example, your local branch moves from `C` to `E`:

Before `git pull`

`A` → `B` → `C`

After `git pull` (fast-forward)

`A` → `B` → `C` →&#x20;

&#x20;`D` → `E`

Now your local `main` branch includes the remote commits.

When should you use `git pull`?

- You want to update your local branch with the latest remote changes.
- You are starting work on a project and want the latest code.
- You want a straightforward way to synchronize your branch with its configured upstream branch.
- You have checked that your current work is ready for integration.

## 3. Side-by-side comparison

| Feature                                          | `git fetch`                      | `git pull`                             |
| ------------------------------------------------ | -------------------------------- | -------------------------------------- |
| Downloads remote changes                         | Yes                              | Yes                                    |
| Updates remote-tracking references               | Yes                              | Yes                                    |
| Integrates changes into your current branch      | No                               | Yes                                    |
| Changes your working files automatically         | No                               | Potentially                            |
| Lets you inspect changes first                   | Yes                              | Not before integration                 |
| Requires a separate merge or rebase to integrate | Usually, if you want the changes | No, integration is part of the command |
| Best for                                         | Control and inspection           | Convenience and synchronization        |

## 4. Why might your professor recommend `git pull` over `git fetch`?

Your professor's recommendation makes sense, particularly if you are learning Git or working on a relatively straightforward project.

There are three main reasons.

### A. It is simpler

Instead of running two commands:

```
git fetch
git merge
```

You can often use just:

```
git pull
```

This makes it easier to keep your local branch current without having to remember a separate integration step.

### B. It helps you start with the latest code

Imagine you are working on a team project with a shared GitHub repository.

Another student updates `main` with a bug fix. Before you begin your next task, you run:

```
git switch main
git pull
```

Your local `main` branch is updated with the latest remote changes, assuming the pull succeeds and your configuration is appropriate.

This reduces the chance of starting new work from an outdated version of the project.

### C. It reduces the chance of forgetting to integrate updates

If you run `git fetch` but forget to merge or rebase afterward, your local branch will remain behind the remote branch.

`git pull` combines those steps, so this is less likely to happen.

However, `git pull` is not inherently safer or better than `git fetch`. It integrates changes immediately, which can be inconvenient if you wanted to review them first.

## 5. Is `git pull` always the best choice?

No. It depends on your situation.

Consider these scenarios:

Scenario 1: You are beginning a coding session

Recommended: `git pull`

You want to get the latest changes before starting work.

Scenario 2: You want to see what a teammate changed

Recommended: `git fetch`

You can inspect incoming commits and differences before integrating them.

Scenario 3: You are working on a shared branch and want to synchronize

Recommended: Usually `git pull`

It is convenient, provided you understand your team's merge or rebase policy and have committed or otherwise protected your own work.

One important caution: if your local branch and the remote branch have diverged, `git pull` may require a merge or rebase decision. Conflicts can occur if both sides changed the same parts of a file. Git generally will not silently discard your committed work, but you may need to resolve conflicts before continuing.

## 6. A practical workflow for your coursework

For a typical student project using GitHub, a reasonable workflow is:

```
# 1. Switch to your main branch
git switch main

# 2. Get the latest changes
git pull

# 3. Create a branch for your task
git switch -c feature/my-task

# 4. Make changes and stage them
git add .

# 5. Commit your changes
git commit -m "Add my task"

# 6. Push your branch to GitHub
git push -u origin feature/my-task
```

This assumes your team uses `main` as its shared base branch and that you are allowed to pull directly into it. If your instructor or team requires pull requests, this workflow lets you develop on your own branch before proposing your changes for integration.

One additional point: if you have uncommitted work before pulling, check its status first:

```
git status
```

Commit your work or otherwise protect it before integrating remote changes. Git can sometimes pull safely with uncommitted changes, but it may refuse if those changes would be overwritten.

## 7. Test your understanding

Question: Another student pushes three new commits to GitHub. You want to download those commits but inspect them before changing your current local branch. Which command should you use?

`git pull`

`git fetch`

`git push`

Check answer

## Bottom line

- Use `git pull` when you want to download and integrate remote changes in one step.
- Use `git fetch` when you want to download remote changes and review them before integration.

Your professor's advice is a reasonable default for everyday student development. As you gain experience, learning when to use `git fetch` will give you more control over collaboration and avoid integrating changes before you are ready.

## Day 5’s Question

What are alternatives to github?Please put your answer into a markdown format.

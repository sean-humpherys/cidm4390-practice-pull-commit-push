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

## Day 2’s Question

What are best practices regarding how often to commit and push, including recommended frequency? Please put your answer into a markdown format.

# Best Practices for Committing and Pushing Code

## How Often Should You Commit?

A good practice is to **commit frequently whenever you complete a small, logical piece of work**.

### Recommended Frequency

- **Commit:** After completing a small, working change, typically every **15–60 minutes** of active development.
- **Push:** At least **several times per day**, or whenever you reach a meaningful checkpoint.
- **Before stopping work:** Push your latest commits so your work is backed up remotely.

> **Rule of thumb:** Make commits **small and meaningful**, rather than making one large commit at the end of the day.

## What Makes a Good Commit?

Each commit should represent **one logical change**.

## Day 3’s Question

Explain branches in git and their best practices? Please put your answer into a markdown format.

# Understanding Git Branches and Best Practices

## 1. What Is a Branch in Git?

A **branch** is an independent line of development in a Git repository. It allows developers to work on new features, fix bugs, or experiment with changes without immediately affecting the main version of the project.

Think of a branch as a separate workspace for your code. You can make changes and commit them without changing the code in other branches.

### Example

Imagine a team developing a library website. The repository has a main branch and two feature branches:

- `main` — Contains the stable, approved version of the website.
- `feature/search-bar` — Used to develop a new search bar.
- `bugfix/login-error` — Used to fix a login problem.

Each developer can work on their branch independently. Once their work is complete and reviewed, it can be merged into `main`.

# Git Branch Best Practices

1. **Avoid working directly on `main`.** Create a separate branch for each feature, bug fix, or task to protect the stable version of the project.

2. **Use descriptive branch names.** Choose names that explain the purpose of the work, such as `feature/book-search` or `bugfix/login-error`.

3. **Create branches from the latest `main`.** Update your local `main` branch before starting a new task to reduce potential merge conflicts.

4. **Keep branches focused and short-lived.** Work on one task per branch and merge it as soon as it is complete and reviewed. Aim for a day or a few days when practical.

5. **Commit frequently.** Commit small, logical units of work with clear messages describing the changes.

6. **Push branches regularly.** Push commits at meaningful checkpoints and before ending a work session to back up your work and share progress.

7. **Keep branches updated.** Regularly incorporate changes from `main` into your feature branch so conflicts can be identified and resolved early.

8. **Use pull requests and code reviews.** Have teammates review changes and run appropriate tests before merging into `main`.

9. **Resolve merge conflicts carefully.** Review conflicting code, preserve necessary changes from both developers, and test the result before merging.

10. **Protect the `main` branch.** Use branch protection rules, required reviews, and automated tests when supported by your repository platform.

11. **Avoid force-pushing to shared branches.** Rewriting shared history can disrupt teammates' work or remove commits from the branch history.

12. **Delete merged branches.** Remove local and remote branches that are no longer needed to keep the repository organized.

## Recommended Workflow

1. Update `main` with the latest changes.
2. Create a branch for your task.
3. Make changes and test them.
4. Commit and push your work regularly.
5. Open a pull request.
6. Review the code and resolve conflicts.
7. Merge the approved changes into `main`.
8. Delete the completed branch.

## Day 4’s Question

What is the difference between git pull and git fetch? My professor advises using git pull over git fetch? Can you put your answer into a markdown format please.

**Explanation:** `git fetch` downloads the latest commits and updates from a remote repository without integrating them into your current branch.

- **Downloads updates:** Retrieves new commits and information from the remote repository.
- **Does not merge changes:** Your current branch and working files remain unchanged by the fetch itself.
- **Allows inspection:** You can review incoming changes before deciding to merge or rebase them.
- **Best used when:** You want to see what teammates have changed before incorporating their work.

**Explanation** `git pull` downloads updates from a remote repository and integrates them into your current branch.

- **Downloads updates:** Retrieves new commits and information from the remote repository.
- **Integrates changes:** Incorporates remote changes into your current branch through merging or rebasing, depending on your Git          configuration.
- **May cause merge conflicts:** If changes overlap, you may need to resolve conflicts before continuing.
- **Best used when:** You want to update your current branch with the latest remote changes and continue working.

## Day 5’s Question

What are alternatives to github?Please put your answer into a markdown format.

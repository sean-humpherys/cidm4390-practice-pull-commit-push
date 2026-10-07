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

### What Happens:
1. A pushes first: succeeds.
2. B's push is rejected: B's local main is behind the remote (! [rejected] main -> main (fetch first)).
3. B must integrate A's work: git pull or git pull --rebase.
- Different regions of the file: Git auto-merges.
- Same or adjacent lines: merge conflict; B resolves it manually.

### Consequences:
- Delay and manual effort for the second coder
- Possible extra merge commit in history,
- Semantic conflicts: a clean auto-merge can still break the code,
- Bad resolution: A's changes can be accidentally dropped,
- Broken main: if the merge isn't built and tested before pushing,
- git push --force: erases A's commits from the remote.

## Day 2’s Question

What are best practices regarding how often to commit and push, including recommended frequency? Please put your answer into a markdown format.

### Git Commit and Push Frequency

#### Commit
- Commit after each small, logical change (several per hour while actively developing).
- One logical change per commit.
- Don't commit broken code to shared branches.
- Avoid giant end-of-day commits.

#### Push
- Push at least once per working day.
- Ideally push after each meaningful milestone (a completed feature or passing tests).
- Pull before you push on shared branches.

## Day 3’s Question

Explain branches in git and their best practices? Please put your answer into a markdown format.

### Git Branches

#### What Is a Branch
- A movable pointer to a commit that lets you work in isolation from `main`.

#### Best Practices
- Keep `main` stable; it should always build and pass tests.
- Use one branch per feature, fix, or experiment, with clear names (`feature/login-page`).
- Keep branches short-lived and pull from `main` regularly to avoid conflicts.
- Use pull requests, code review, and CI before merging.
- Protect `main` (required reviews, passing CI, no force-push).
- Delete branches after merging.

## Day 4’s Question

What is the difference between git pull and git fetch? My professor advises using git pull over git fetch? Can you put your answer into a markdown format please.

## Day 5’s Question

What are alternatives to github?Please put your answer into a markdown format.

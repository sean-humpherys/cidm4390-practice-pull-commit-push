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

When two developers work directly on `main`, modify the same file, commit, and attempt to push at different times, the outcome depends entirely on **who pushes first** and **which parts of the file were edited**.

---

### 1. What Happens to the First Developer (Coder A)

* **Experience:** Coder A pushes their commit without issue.
* **Result:** Their changes become the official tip of `main` on the remote repository.

---

### 2. What Happens to the Second Developer (Coder B)

* **The Push Fails:** When Coder B runs `git push`, Git rejects it with a non-fast-forward error:
```text
[rejected]        main -> main (fetch first)
error: failed to push some refs to '<remote-url>'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally.

```


* **Git never silently overwrites Coder A's work.** Git requires Coder B to pull the remote changes and integrate them locally before pushing.

---

### 3. Resolving the Integration (When Coder B Pulls)

Coder B must run `git pull` (or `git fetch` followed by `git merge` / `git rebase`). At this stage, one of two scenarios occurs:

| Scenario | What Happened | Outcome |
| --- | --- | --- |
| **Different lines modified** | Coder A and Coder B edited different functions, lines, or sections of the same file. | **Auto-Merge Succeeded:** Git automatically combines both sets of changes. A merge commit is created (or commits are replayed cleanly if using rebase). Coder B can then push. |
| **Overlapping lines modified** | Both coders edited the exact same line(s) or conflicting blocks of code. | **Merge Conflict:** Git halts the process and marks conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`) directly inside the file. Coder B must manually decide which code to keep. |

---

### 4. Technical and Project Consequences

* **Merge Conflicts Require Manual Resolution:** If conflicts occur, Coder B must manually inspect the code, consult Coder A if necessary, edit the conflict markers out, stage the file (`git add`), and complete the merge/rebase.
* **Silent Logical Conflicts:** Even if Git auto-merges cleanly because the edits were on different lines, the code can still break logically (e.g., Coder A renamed a function or variable that Coder B just implemented elsewhere in the same file). If automated tests or manual builds aren't run prior to pushing, broken code lands on `main`.
* **Cluttered History:** Repeated direct pushes and automatic merges directly on `main` generate a tangled commit graph ("foxtrot merges") rather than a clean, traceable history.

---

### Recommended Best Practice

To prevent these conflicts on shared codebases:

1. **Feature Branches:** Never commit directly to `main`. Work on feature branches (e.g., `feature/update-auth`).
2. **Pull Requests (PRs):** Merge into `main` via PRs with branch protection rules enabled, requiring automated tests (CI) and peer reviews before code can merge.
3. **Rebase/Pull Often:** Keep local branches synchronized with `main` frequently to catch diverging edits early.

## Day 2’s Question

What are best practices regarding how often to commit and push, including recommended frequency? Please put your answer into a markdown format.

## Day 3’s Question

Explain branches in git and their best practices? Please put your answer into a markdown format.

## Day 4’s Question

What is the difference between git pull and git fetch? My professor advises using git pull over git fetch? Can you put your answer into a markdown format please.

## Day 5’s Question

What are alternatives to github?Please put your answer into a markdown format.

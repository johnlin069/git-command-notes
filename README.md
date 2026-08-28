# Git Command Notes

Personal Git command cheat sheet for daily development work.

---

## 1. Basic

### Check repository status
```bash
git status
```

### View commit history
```bash
git log --oneline
```

### View commit graph
```bash
git log --oneline --graph --all --decorate
```

### Check current branch
```bash
git branch --show-current
```

### Check remote repository
```bash
git remote -v
```

---

## 2. Add & Commit

### Add all changes
```bash
git add .
```

### Add specific file
```bash
git add <file>
```

### Commit
```bash
git commit -m "Commit message"
```

### Modify the latest commit message
```bash
git commit --amend -m "New commit message"
```

---

## 3. Push & Pull

### Push current branch
```bash
git push
```

### First push of a new branch
```bash
git push -u origin <branch_name>
```

### Pull latest changes
```bash
git pull
```

### Fetch remote changes without merging
```bash
git fetch
```

---

## 4. Branch

### List branches
```bash
git branch
```

### List local and remote branches
```bash
git branch -a
```

### Create a new branch
```bash
git branch <branch_name>
```

### Create and switch to a new branch
```bash
git switch -c <branch_name>
```

Alternative:
```bash
git checkout -b <branch_name>
```

### Switch branch
```bash
git switch <branch_name>
```

### Delete local branch
```bash
git branch -d <branch_name>
```

### Force delete local branch
```bash
git branch -D <branch_name>
```

---

## 5. Create Branch From Specific Commit

Useful when you want to keep the current development branch unchanged and start another branch from an older commit.

### Check commit history
```bash
git log --oneline --graph --all
```

Example:
```text
43dc440 Timing Report and Simulation Gitignore
a259151 Feature Support : C41AC and Bios Staging
2c64548 Update .gitignore and remove generated files
```

### Create branch from specific commit
```bash
git switch -c <new_branch> <commit_id>
```

Example:
```bash
git switch -c new_feature 2c64548
```

Alternative:
```bash
git checkout -b new_feature 2c64548
```

### Push the new branch
```bash
git push -u origin new_feature
```

---

## 6. Undo / Restore

### Discard changes in one file
```bash
git restore <file>
```

### Discard all unstaged changes
```bash
git restore .
```

### Unstage a file
```bash
git restore --staged <file>
```

### Unstage everything
```bash
git restore --staged .
```

---

## 7. Reset

> Warning: `reset --hard` can permanently discard local changes.

### Move HEAD back but keep changes staged
```bash
git reset --soft <commit_id>
```

### Move HEAD back and keep changes unstaged
```bash
git reset <commit_id>
```

### Completely return to a commit
```bash
git reset --hard <commit_id>
```

Example:
```bash
git reset --hard 2c64548
```

### Make remote branch match local branch
```bash
git push --force-with-lease
```

Prefer `--force-with-lease` over `--force` when rewriting remote history.

---

## 8. Revert

Use `revert` when the commit has already been shared and you want to undo it without rewriting history.

```bash
git revert <commit_id>
```

Example:
```bash
git revert a259151
```

---

## 9. Stash

### Temporarily save current changes
```bash
git stash
```

### Save with description
```bash
git stash push -m "Work in progress"
```

### View stash list
```bash
git stash list
```

### Restore latest stash
```bash
git stash pop
```

### Apply without deleting stash
```bash
git stash apply
```

---

## 10. Merge

### Switch to target branch
```bash
git switch main
```

### Merge another branch
```bash
git merge <branch_name>
```

Example:
```bash
git merge feature_branch
```

---

## 11. Cherry-pick

Apply one specific commit from another branch.

```bash
git cherry-pick <commit_id>
```

Example:
```bash
git cherry-pick a259151
```

---

## 12. Tag

### List tags
```bash
git tag
```

### Create tag
```bash
git tag <tag_name>
```

### Create annotated tag
```bash
git tag -a <tag_name> -m "Description"
```

Example:
```bash
git tag -a v02.08.00 -m "Release v02.08.00"
```

### Push one tag
```bash
git push origin <tag_name>
```

### Push all tags
```bash
git push origin --tags
```

### Checkout an old tag
```bash
git checkout <tag_name>
```

> Checking out a tag normally puts Git into detached HEAD state.

To develop from that tag:
```bash
git switch -c <new_branch> <tag_name>
```

---

## 13. Compare Changes

### Check unstaged changes
```bash
git diff
```

### Check staged changes
```bash
git diff --staged
```

### Compare two commits
```bash
git diff <commit_A> <commit_B>
```

### Show files changed between two commits
```bash
git diff --name-only <commit_A> <commit_B>
```

---

## 14. Remote

### Show remote repositories
```bash
git remote -v
```

### Add remote
```bash
git remote add origin <repository_url>
```

### Change remote URL
```bash
git remote set-url origin <repository_url>
```

---

## 15. Useful Daily Workflow

```bash
git status
git pull
git add .
git commit -m "Update feature"
git push
```

For a new branch:

```bash
git switch -c feature_name
git add .
git commit -m "Add feature"
git push -u origin feature_name
```

---

## Quick Reference

| Goal | Command |
|---|---|
| Status | `git status` |
| History | `git log --oneline --graph --all` |
| Current branch | `git branch --show-current` |
| New branch | `git switch -c <branch>` |
| Branch from commit | `git switch -c <branch> <commit>` |
| Add everything | `git add .` |
| Commit | `git commit -m "message"` |
| Push | `git push` |
| Pull | `git pull` |
| Undo shared commit | `git revert <commit>` |
| Hard reset | `git reset --hard <commit>` |
| Save temporary work | `git stash` |
| Restore stash | `git stash pop` |
| Apply one commit | `git cherry-pick <commit>` |
| Create tag | `git tag -a <tag> -m "message"` |
| Push tags | `git push origin --tags` |

# Git Status, Log, and Diff: Tracking Changes Effectively

This guide covers three essential Git commands: `git status`, `git log`, and `git diff`. These commands help you monitor changes, review commit history, and compare differences, making it easier to manage and track project progress.

---

## 1. Understanding `git status`, `git log`, and `git diff`

- **`git status`:** Displays the state of the working directory and staging area.
- **`git log`:** Shows commit history, including author information and timestamps.
- **`git diff`:** Compares changes between commits, the staging area, and working directory.

> **Tip:** Regularly using these commands ensures a clean and well-managed repository.

---

## 2. Using `git status`

### 2.1 Checking the Current Status:
```bash
git status
```
Displays:
- Files staged for commit
- Unstaged changes
- Untracked files

### 2.2 Viewing Status with Short Format:
```bash
git status -s
```
Example output:
```
 M modified-file.ext
?? untracked-file.ext
```

### 2.3 Understanding Output Symbols:
- `M`: Modified
- `A`: Added
- `D`: Deleted
- `??`: Untracked

---

## 3. Exploring `git log`

### 3.1 Basic Commit History:
```bash
git log
```
Shows commit hash, author, date, and message.

### 3.2 One-Line Summary:
```bash
git log --oneline
```
Provides a condensed view of commits.

### 3.3 Visualizing Commit Graph:
```bash
git log --oneline --graph --decorate --all
```
Useful for understanding branch merges and history.

### 3.4 Filtering Logs:
```bash
git log --author="Author Name"
git log --since="2 weeks ago"
git log --grep="Keyword"
```

> **Tip:** Combine options for precise history tracking.

---

## 4. Comparing Changes with `git diff`

### 4.1 Comparing Working Directory and Staging Area:
```bash
git diff
```
Shows differences not yet staged.

### 4.2 Comparing Staged Changes:
```bash
git diff --staged
```
Displays staged changes relative to the last commit.

### 4.3 Comparing Commits:
```bash
git diff commit1 commit2
```
Replace `commit1` and `commit2` with actual commit hashes.

### 4.4 Showing Word-Level Differences:
```bash
git diff --word-diff
```
Useful for analyzing changes in text content.

---

## 5. Advanced Usage of Status, Log, and Diff

### 5.1 Viewing Specific File History:
```bash
git log -- <filename>
```

### 5.2 Checking Differences for Specific Files:
```bash
git diff HEAD~1 HEAD -- <filename>
```

### 5.3 Searching Commit Messages:
```bash
git log --grep="Fix bug"
```

---

## 6. Best Practices for Using `git status`, `git log`, and `git diff`

- **Use `git status` frequently:** Stay aware of uncommitted changes.
- **Review commit history with `git log`:** Understand the evolution of the project.
- **Leverage `git diff` before commits:** Ensure only intended changes are committed.
- **Combine flags for clarity:** `git log --oneline --graph` provides a neat visual history.

---

## 7. Troubleshooting Common Issues

### 7.1 Changes Missing from Diff:
- Confirm correct commit references when using `git diff`.

### 7.2 Confusing Commit History:
- Use graphical visualization: `git log --graph --oneline --decorate`.

### 7.3 Unstaged Changes Overwritten:
- Run `git stash` before switching branches to save work-in-progress.

---

## Summary

- **`git status`:** Provides real-time information about the repository state.
- **`git log`:** Tracks and reviews commit history.
- **`git diff`:** Compares changes across commits, staging, and working directories.

Mastering these commands enables effective change tracking, smooth collaboration, and a well-documented project history.

---

Track, Review, and Compare—Master Git Insights! 🚀✨


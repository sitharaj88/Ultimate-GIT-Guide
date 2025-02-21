# Git Hooks: Automating Workflows in Git

This guide explores Git hooks, their use cases, and how to implement them to automate key parts of the Git workflow. Hooks allow custom scripts to run automatically at specific points in the Git lifecycle, enhancing efficiency and maintaining code quality.

---

## 1. Understanding Git Hooks

### 1.1 What Are Git Hooks?

Git hooks are executable scripts triggered by specific Git events, such as commits, merges, or pushes. They enable automation of tasks like code linting, running tests, or enforcing commit message standards.

### 1.2 Why Use Git Hooks?
- **Automated Code Quality Checks:** Run linters and tests before commits or pushes.
- **Consistent Commit Messages:** Enforce formatting standards.
- **Deployment Automation:** Trigger deployments post-push.
- **Prevention of Bad Code Pushes:** Reject pushes that don’t meet certain criteria.

> **Tip:** Git hooks live in the `.git/hooks` directory of a repository.

---

## 2. Types of Git Hooks

### 2.1 Client-Side Hooks
These run on the developer's machine:
- **pre-commit:** Run before a commit is made (e.g., run linters, tests).
- **prepare-commit-msg:** Modify the commit message template.
- **commit-msg:** Validate commit messages.
- **pre-push:** Run tests or checks before pushing.
- **post-commit:** Actions after a successful commit (e.g., notifications).

### 2.2 Server-Side Hooks
These run on the server where the repository is hosted:
- **pre-receive:** Check conditions before accepting a push.
- **update:** Runs once per branch pushed.
- **post-receive:** Trigger CI/CD pipelines or notifications.

---

## 3. Setting Up Git Hooks

### 3.1 Creating a Hook
1. Navigate to `.git/hooks/` in your repository.
2. Create a new file named after the desired hook (e.g., `pre-commit`).
3. Make it executable:
```bash
chmod +x .git/hooks/pre-commit
```
4. Add the desired script:
```bash
#!/bin/sh
npm run lint
```
*Use case:* Prevent commits if linting fails.

### 3.2 Example: Commit Message Validation
```bash
#!/bin/sh
commit_msg=$(cat $1)
if ! echo "$commit_msg" | grep -qE "^(feat|fix|docs|style|refactor|test|chore): "; then
  echo "Aborting commit. Your commit message must follow Conventional Commits."
  exit 1
fi
```
*Use case:* Enforce consistent commit messages.

---

## 4. Sharing Git Hooks Across Teams

### 4.1 Using `core.hooksPath`
Set a custom hooks directory that can be version-controlled:
```bash
git config core.hooksPath .githooks
```

### 4.2 Creating a Shared Hooks Directory
1. Create `.githooks/` at the project root.
2. Add hooks scripts there.
3. Commit `.githooks/` to the repository.

> **Tip:** This approach ensures all team members use the same hooks.

### 4.3 Installing Shared Hooks Automatically
Add this to the project's `package.json`:
```json
"scripts": {
  "postinstall": "git config core.hooksPath .githooks"
}
```

---

## 5. Advanced Git Hooks Use Cases

### 5.1 Pre-Push Testing
```bash
#!/bin/sh
npm test
if [ $? -ne 0 ]; then
  echo "Tests failed. Push aborted."
  exit 1
fi
```
*Use case:* Block pushes if tests fail.

### 5.2 Post-Merge Actions
```bash
#!/bin/sh
npm install
```
*Use case:* Automatically install dependencies after a merge.

### 5.3 Post-Receive CI Trigger
```bash
#!/bin/sh
curl -X POST https://ci.example.com/job/build/trigger
```
*Use case:* Trigger a CI build when a push is received.

---

## 6. Best Practices for Git Hooks

- **Keep Hooks Fast:** Avoid slow operations in critical hooks like `pre-commit`.
- **Fail Fast:** Hooks should exit with non-zero status on failure.
- **Use Tools for Complex Workflows:** Tools like Husky can simplify managing hooks.
- **Version-Control Hooks:** Use `core.hooksPath` to keep hooks under version control.
- **Document Hooks:** Clearly explain hook behaviors in project documentation.

---

## 7. Troubleshooting Git Hooks

### 7.1 Hook Not Running
- Ensure the hook file is executable (`chmod +x`).
- Verify the file has no extensions (e.g., `pre-commit.sh` will not work).

### 7.2 Debugging Failing Hooks
- Add debug statements (`echo "Debug info"`) to the script.
- Run hooks manually to identify issues:
```bash
.git/hooks/pre-commit
```

### 7.3 Shared Hook Not Triggering
- Confirm `core.hooksPath` is set correctly.
- Reinstall dependencies if using package managers with hook support.

---

## 8. Real-World Use Cases

- **Linting Before Commits:** Ensure code consistency.
- **Testing Before Pushes:** Prevent broken code from reaching shared branches.
- **CI/CD Triggers:** Automate deployment workflows.
- **Security Checks:** Run security scans before merges.
- **Documentation Enforcement:** Ensure updated documentation with code changes.

---

## Summary

- **Create Hooks:** Add scripts to `.git/hooks/` or a custom path.
- **Make Executable:** Use `chmod +x`.
- **Share Hooks:** Leverage `core.hooksPath` for team consistency.
- **Automate Workflows:** Use hooks for linting, testing, and CI/CD triggers.

Git hooks are powerful tools for automating processes, enforcing standards, and ensuring code quality. Mastering hooks can lead to efficient and error-free workflows across any development team.

---

Automate, Standardize, and Simplify—Master Git Hooks! 🚀✨


# Git Hook Scripts: Automating Tasks and Enhancing Git Workflows

This section provides **practical Git hook script examples** that automate processes, enforce code quality, and streamline workflows. Git hooks are customizable scripts that Git executes at specific points in the Git lifecycle.

---

## 1. Understanding Git Hooks

### 1.1 What Are Git Hooks?

**Git hooks** are scripts that run automatically on Git commands such as commit, push, and merge. They can be used to enforce coding standards, automate testing, and enhance project workflows.

### 1.2 Why Use Git Hooks?
- **Enforce Standards:** Ensure consistent commit messages and code quality.
- **Automate Tasks:** Run tests, lint code, or generate documentation automatically.
- **Prevent Mistakes:** Block commits with sensitive data or failing tests.

> **Tip:** Git hooks are stored in the `.git/hooks` directory and need to be executable.

---

## 2. Common Git Hook Scripts

### 2.1 pre-commit
- **Purpose:** Run checks before a commit is recorded.
- **Example: Lint Check Before Commit**
  ```bash
  #!/bin/sh
  echo "Running lint checks..."
  npm run lint
  if [ $? -ne 0 ]; then
    echo "Linting failed. Commit aborted."
    exit 1
  fi
  ```

### 2.2 commit-msg
- **Purpose:** Validate commit message format.
- **Example: Enforce Commit Message Format**
  ```bash
  #!/bin/sh
  COMMIT_MSG_FILE=$1
  REGEX="^(feat|fix|docs|style|refactor|test|chore): .+$"
  if ! grep -qE "$REGEX" "$COMMIT_MSG_FILE"; then
    echo "Invalid commit message. Use 'type: description' format."
    exit 1
  fi
  ```

### 2.3 pre-push
- **Purpose:** Run tests before pushing to a remote.
- **Example: Run Tests Before Push**
  ```bash
  #!/bin/sh
  echo "Running tests before push..."
  npm test
  if [ $? -ne 0 ]; then
    echo "Tests failed. Push aborted."
    exit 1
  fi
  ```

### 2.4 pre-rebase
- **Purpose:** Prevent rebase if local changes are present.
- **Example: Rebase Check**
  ```bash
  #!/bin/sh
  if ! git diff-index --quiet HEAD --; then
    echo "Uncommitted changes found. Rebase aborted."
    exit 1
  fi
  ```

---

## 3. Advanced Git Hook Scripts

### 3.1 post-merge
- **Purpose:** Install dependencies after merge.
- **Example: Install Dependencies**
  ```bash
  #!/bin/sh
  echo "Installing dependencies after merge..."
  npm install
  ```

### 3.2 post-checkout
- **Purpose:** Run actions after switching branches.
- **Example: Notify Branch Change**
  ```bash
  #!/bin/sh
  echo "Switched to branch: $(git rev-parse --abbrev-ref HEAD)"
  ```

### 3.3 pre-commit: Prevent Sensitive Data
- **Purpose:** Block commits containing sensitive data.
- **Example: Check for API Keys**
  ```bash
  #!/bin/sh
  if grep -r "API_KEY" *; then
    echo "API key detected! Commit rejected."
    exit 1
  fi
  ```

---

## 4. Setting Up Git Hooks

### 4.1 Creating a Hook
- Navigate to `.git/hooks`:
  ```bash
  cd .git/hooks
  ```
- Create the hook file:
  ```bash
  touch pre-commit
  ```
- Add script and make executable:
  ```bash
  chmod +x pre-commit
  ```

### 4.2 Sharing Hooks Across Teams
- Store hooks in a shared directory:
  ```bash
  mkdir -p .githooks
  ```
- Configure Git to use custom hooks path:
  ```bash
  git config core.hooksPath .githooks
  ```

---

## 5. Best Practices for Git Hooks

- **Keep Scripts Fast:** Slow hooks can disrupt workflows.
- **Document Hook Usage:** Help teams understand hook purpose and actions.
- **Use Pre-commit Hooks for Linting:** Ensure consistent code quality.
- **Integrate with CI/CD:** Use hooks to trigger pipeline processes.
- **Test Hooks Thoroughly:** Prevent unintended side effects.

---

## 6. Troubleshooting Git Hooks

### 6.1 Hook Not Executing
- Ensure script is executable:
  ```bash
  chmod +x .git/hooks/<hook-name>
  ```
- Confirm `core.hooksPath` is set correctly:
  ```bash
  git config --get core.hooksPath
  ```

### 6.2 Debugging Hook Failures
- Add debug output to hook scripts:
  ```bash
  echo "Debug Info: Running pre-commit hook..."
  ```

### 6.3 Hook Conflicts
- Coordinate with team members on hook requirements.
- Use shared hook directories for consistency.

---

## 7. Real-World Use Cases

- **Enforcing Code Standards:** Use `pre-commit` hooks for linting and formatting.
- **CI/CD Integrations:** Trigger automated testing pipelines with `pre-push` hooks.
- **Sensitive Data Protection:** Detect secrets in code using custom `pre-commit` scripts.
- **Post-Deployment Checks:** Use `post-merge` hooks to ensure environments are up-to-date.

---

## 8. Summary

- **Automate with Hooks:** Use Git hooks to streamline workflows and enforce standards.
- **Create Reusable Scripts:** Share hooks with your team for consistent operations.
- **Secure Commits:** Block sensitive data and enforce commit standards.
- **Integrate Seamlessly:** Connect Git hooks with CI/CD pipelines for robust automation.

Git hooks are powerful tools for automating and securing Git workflows. By mastering hook scripts, teams can ensure code quality, streamline operations, and reduce errors.

---

Automate, Secure, Optimize—Master Git Hook Scripts for Seamless Development! 🚀✨


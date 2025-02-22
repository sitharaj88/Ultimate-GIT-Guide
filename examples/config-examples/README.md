# Git Config Examples: Practical Configurations for Efficient Git Workflows

This section provides **practical Git configuration examples** that enhance productivity, streamline workflows, and secure Git operations. These configurations cover user settings, aliases, performance optimizations, and security enhancements.

---

## 1. User Identity Configuration

### 1.1 Setting User Name and Email
- **Global Configuration:**
  ```bash
  git config --global user.name "Your Name"
  git config --global user.email "you@example.com"
  ```

- **Local Configuration:** (Overrides global settings for a specific repository)
  ```bash
  git config user.name "Repo Specific Name"
  git config user.email "repo@example.com"
  ```

---

## 2. Core Editor Configuration

### 2.1 Setting Default Editor
- **Vim:**
  ```bash
  git config --global core.editor "vim"
  ```
- **Visual Studio Code:**
  ```bash
  git config --global core.editor "code --wait"
  ```
- **Sublime Text:**
  ```bash
  git config --global core.editor "subl -n -w"
  ```

---

## 3. Alias Configuration

### 3.1 Useful Git Aliases
- **Shorten Common Commands:**
  ```bash
  git config --global alias.co checkout
  git config --global alias.br branch
  git config --global alias.cm commit
  git config --global alias.st status
  git config --global alias.lg "log --oneline --graph --all"
  ```

- **Undo Last Commit:**
  ```bash
  git config --global alias.uncommit "reset --soft HEAD~1"
  ```

- **Amend Commits:**
  ```bash
  git config --global alias.amend "commit --amend"
  ```

---

## 4. Credential Management Configuration

### 4.1 Storing Credentials Securely
- **Credential Manager:**
  ```bash
  git config --global credential.helper manager-core
  ```
- **Credential Cache (Temporary Storage):**
  ```bash
  git config --global credential.helper 'cache --timeout=3600'
  ```
- **Credential Store (Persistent Storage):**
  ```bash
  git config --global credential.helper store
  ```

---

## 5. Performance Optimization

### 5.1 Adjusting Git Performance Settings
- **Compression Level:**
  ```bash
  git config --global core.compression 9
  ```
- **Parallel Fetching:**
  ```bash
  git config --global pack.threads 4
  ```

### 5.2 Garbage Collection
- **Automatic Garbage Collection Settings:**
  ```bash
  git config --global gc.auto 256
  git config --global gc.pruneExpire "1.month.ago"
  ```

---

## 6. Security Enhancements

### 6.1 GPG Signing for Commits
- **Enable GPG Signing:**
  ```bash
  git config --global commit.gpgsign true
  ```
- **Set GPG Key:**
  ```bash
  git config --global user.signingkey <GPG-KEY-ID>
  ```

### 6.2 SSH Configuration
- **Check SSH Setup:**
  ```bash
  ssh -T git@github.com
  ```
- **Configure SSH Key:**
  ```bash
  eval "$(ssh-agent -s)"
  ssh-add ~/.ssh/id_rsa
  ```

---

## 7. Proxy Configuration

### 7.1 Configuring Git to Use a Proxy
- **HTTP Proxy:**
  ```bash
  git config --global http.proxy http://proxy.example.com:8080
  ```
- **HTTPS Proxy:**
  ```bash
  git config --global https.proxy https://proxy.example.com:8080
  ```
- **Remove Proxy Settings:**
  ```bash
  git config --global --unset http.proxy
  git config --global --unset https.proxy
  ```

---

## 8. Diff and Merge Tool Configuration

### 8.1 Setting Up Diff Tools
- **Meld as Diff Tool:**
  ```bash
  git config --global diff.tool meld
  ```

### 8.2 Setting Up Merge Tools
- **Meld as Merge Tool:**
  ```bash
  git config --global merge.tool meld
  ```

---

## 9. Core Git Behavior Configurations

### 9.1 Case Sensitivity
- **Enable/Disable Case Sensitivity:**
  ```bash
  git config --global core.ignorecase false
  ```

### 9.2 Auto Correct Mistyped Commands
- **Enable Auto Correct:**
  ```bash
  git config --global help.autocorrect 1
  ```

### 9.3 Line Ending Normalization
- **Ensure Consistent Line Endings:**
  ```bash
  git config --global core.autocrlf input
  ```

---

## 10. Viewing and Managing Configurations

### 10.1 View Current Configurations
- **Global Configurations:**
  ```bash
  git config --global --list
  ```
- **Local Configurations:**
  ```bash
  git config --list
  ```

### 10.2 Editing Config Files Directly
- **Global Config:**
  ```bash
  git config --global -e
  ```
- **Local Config:**
  ```bash
  git config -e
  ```

---

## Summary

This configuration guide includes practical Git settings for user identity, performance optimization, credential management, security enhancements, and tool integrations. Implementing these configurations ensures a streamlined, secure, and efficient Git workflow.

---

Configure, Optimize, Secure—Master Git Configurations for Seamless Development! ⚙️✨


# Managing Multiple Git Accounts: Work and Personal Setup

Working with multiple Git accounts, such as separate work and personal profiles, can be challenging. This guide explains how to manage multiple accounts effectively, ensuring seamless workflow and preventing commit attribution issues.

---

## 1. Why Manage Multiple Git Accounts?

- **Separation of Work and Personal Projects:** Maintain clear boundaries between professional and personal repositories.
- **Different SSH Keys and Credentials:** Prevent authentication issues when accessing different Git hosting services.
- **Consistent Commit Attribution:** Ensure commits are credited to the correct account.

---

## 2. Setting Up SSH Keys for Multiple Accounts

### 2.1 Generate SSH Keys for Each Account

#### Personal Account:
```bash
ssh-keygen -t rsa -b 4096 -C "personal_email@example.com" -f ~/.ssh/id_rsa_personal
```

#### Work Account:
```bash
ssh-keygen -t rsa -b 4096 -C "work_email@example.com" -f ~/.ssh/id_rsa_work
```

### 2.2 Add SSH Keys to SSH Agent
```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa_personal
ssh-add ~/.ssh/id_rsa_work
```

### 2.3 Configure SSH Settings in `~/.ssh/config`
```ini
Host github.com-personal
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa_personal

Host github.com-work
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa_work
```

---

## 3. Configuring Git for Multiple Accounts

### 3.1 Global Configuration (for personal account)
```bash
git config --global user.name "Personal Name"
git config --global user.email "personal_email@example.com"
```

### 3.2 Local Repository Configuration (for work repositories)
```bash
cd path/to/work/repository
git config user.name "Work Name"
git config user.email "work_email@example.com"
```

### 3.3 Remote URL Customization
```bash
git remote set-url origin git@github.com-work:workusername/repo.git
```

---

## 4. Managing SSH Keys with Git Hosting Services

### 4.1 GitHub:
- Go to **GitHub > Settings > SSH and GPG keys** and add corresponding SSH keys for each account.

### 4.2 GitLab:
- Navigate to **GitLab > Preferences > SSH Keys** and add each key separately.

---

## 5. Automating Account Switching with Git Aliases

### Create Aliases:
```bash
git config --global alias.work '!git config user.name "Work Name" && git config user.email "work_email@example.com"'

git config --global alias.personal '!git config user.name "Personal Name" && git config user.email "personal_email@example.com"'
```

### Usage:
```bash
git work   # Switch to work account settings
git personal # Switch to personal account settings
```

---

## 6. Credential Management

### Use Git Credential Manager for Seamless Authentication:
```bash
git config --global credential.helper manager-core
```

This ensures Git caches credentials, reducing the need to repeatedly enter usernames and passwords.

---

## 7. Advanced Git Configurations for Multiple Accounts

### Conditional Includes in `~/.gitconfig`:
```ini
[includeIf "gitdir:~/work/"]
    path = ~/.gitconfig-work

[includeIf "gitdir:~/personal/"]
    path = ~/.gitconfig-personal
```

Create separate config files (`~/.gitconfig-work` and `~/.gitconfig-personal`) with account-specific settings.

---

## 8. Troubleshooting Multiple Account Issues

### Common Problems:

- **SSH Key Conflicts:**
  - Ensure the correct SSH key is linked in `~/.ssh/config`.

- **Incorrect Commit Attribution:**
  - Double-check `user.name` and `user.email` in local Git configurations.

- **Authentication Failures:**
  - Use `ssh -T git@github.com-personal` or `ssh -T git@github.com-work` to test connections.

---

## 9. Best Practices for Managing Multiple Git Accounts

- **Consistent Directory Structure:** Organize work and personal repositories in separate directories.
- **Clear Naming Conventions:** Use distinct SSH key names and Git aliases.
- **Document Account Details:** Keep a reference document outlining configurations.
- **Regular Credential Updates:** Rotate SSH keys periodically for enhanced security.

---

## Summary

- Managing multiple Git accounts involves configuring SSH keys, Git user details, and remotes correctly.
- Use `~/.ssh/config` for seamless SSH authentication across accounts.
- Employ Git aliases and conditional includes for easy context switching.
- Follow best practices to prevent authentication issues and commit attribution errors.

With proper configuration, you can work across multiple Git accounts efficiently and securely.

---

Manage Multiple Accounts, Simplify Git! 🚀✨

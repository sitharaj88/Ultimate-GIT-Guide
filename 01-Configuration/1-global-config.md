# Global, System, and Local Git Configuration

Git provides a flexible configuration system that allows you to control every aspect of its behavior. These settings can be defined at three different scopes: **System**, **Global**, and **Local**. Understanding these scopes and how to configure them properly is essential for effective Git usage.

---

## 1. System Configuration

- **Scope:** Applies to every user and repository on the system.
- **Location:** Typically stored in `/etc/gitconfig`. Requires administrative access to modify.
- **Usage:** Set when you want defaults for all users on a machine, such as company-wide policies.

### Common Commands:
```bash
git config --system user.name "System User"
git config --system user.email "system@example.com"
```

### View System Config:
```bash
git config --system --list
```

> **Note:** On some systems, you may need `sudo` to run system-level configurations.

---

## 2. Global Configuration

- **Scope:** Applies to your user account across all repositories on your system.
- **Location:** Stored in the `~/.gitconfig` file on Unix systems or `C:\\Users\\<username>\\.gitconfig` on Windows.
- **Usage:** Ideal for setting personal details, default editors, and behaviors that you want consistent across all projects.

### Essential Global Settings:
```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

### Set Default Editor:
```bash
git config --global core.editor "code --wait"  # For VS Code
git config --global core.editor "nano"          # For Nano
git config --global core.editor "vim"           # For Vim
```

### Configure Line Endings:
```bash
# For Windows
git config --global core.autocrlf true

# For macOS and Linux
git config --global core.autocrlf input
```

### View Global Config:
```bash
git config --global --list
```

---

## 3. Local Configuration

- **Scope:** Specific to a single Git repository.
- **Location:** Found in the `.git/config` file within the repository directory.
- **Usage:** Useful for project-specific settings like custom remotes or merge behaviors.

### Example Local Settings:
```bash
git config user.name "Project Specific Name"
git config user.email "project@example.com"
```

### Customizing Local Behavior:
```bash
# Use a specific merge tool for this project
git config merge.tool vimdiff

# Set a custom remote URL
git config remote.origin.url "git@github.com:user/repo.git"
```

### View Local Config:
```bash
git config --local --list
```

---

## Configuration Precedence

Git resolves configuration conflicts based on the following precedence (highest to lowest):

1. **Local Configuration** (`.git/config`)
2. **Global Configuration** (`~/.gitconfig`)
3. **System Configuration** (`/etc/gitconfig`)

> **Tip:** Local settings override global and system settings when conflicts arise.

---

## Viewing All Configurations with Origins

To see all configuration values along with their source files, use:
```bash
git config --list --show-origin
```

This command helps you debug configuration issues by showing which file each setting originates from.

---

## Editing Configuration Files Directly

While `git config` commands are preferred, you can also edit the config files manually:

- **System Config:** `/etc/gitconfig`
- **Global Config:** `~/.gitconfig`
- **Local Config:** `.git/config` (inside the repository)

Use your preferred text editor to make changes:
```bash
vim ~/.gitconfig  # or use nano, code, etc.
```

---

## Comprehensive List of Git Configurations

### 1. User Information
```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

### 2. Network & Proxy Settings
```bash
# HTTP proxy
git config --global http.proxy http://proxyuser:proxypassword@proxy.server.com:port

# HTTPS proxy
git config --global https.proxy https://proxyuser:proxypassword@proxy.server.com:port

# Disable proxy
git config --global --unset http.proxy
git config --global --unset https.proxy
```

### 3. Core Behavior
```bash
git config --global core.autocrlf input      # Handle line endings
git config --global core.safecrlf true       # Warn about line ending issues
git config --global core.editor "vim"        # Default editor
```

### 4. Credential Management
```bash
git config --global credential.helper cache             # Cache credentials temporarily
git config --global credential.helper 'cache --timeout=3600'  # 1-hour cache
git config --global credential.helper store             # Store credentials permanently
```

### 5. Performance & Optimization
```bash
git config --global pack.threads 4          # Number of threads for packing
```

### 6. Merge and Diff Tools
```bash
git config --global merge.tool vimdiff
git config --global diff.tool meld
```

### 7. Aliases (Shortcuts)
```bash
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.cm "commit -m"
```

### 8. Push & Pull Behavior
```bash
git config --global push.default simple
```

### 9. Security Settings
```bash
git config --global commit.gpgsign true      # Sign commits by default
git config --global user.signingkey <key-id>
```

### 10. UI & Output Formatting
```bash
git config --global color.ui auto
```

---

## Summary

- **System Config:** Machine-wide defaults (admin rights required).
- **Global Config:** User-wide defaults (personal preferences).
- **Local Config:** Project-specific settings (overrides others).

Mastering these configurations ensures a smooth Git experience tailored to your workflow. Adjust them as needed and always verify changes using `git config --list` to avoid surprises.


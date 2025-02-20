# GPG Signing: Sign Your Git Commits for Secure Verification

GPG (GNU Privacy Guard) signing ensures that your Git commits and tags are verifiable and trusted. This guide will walk you through the complete process of setting up GPG keys for Git, configuring Git to sign commits automatically, and troubleshooting common issues.

---

## 1. Introduction to GPG Signing

GPG adds a layer of security by allowing others to verify that your commits came from a trusted source.

### Why Use GPG Signing?
- **Verify Authenticity:** Ensures commits are from the expected author.
- **Prevent Spoofing:** Blocks unauthorized contributors from making fake commits.
- **Build Trust:** Establishes a verifiable commit history.

---

## 2. Installing GPG

### Install GPG on Various Operating Systems:

#### On macOS (using Homebrew):
```bash
brew install gpg
```

#### On Ubuntu/Debian:
```bash
sudo apt update && sudo apt install gnupg
```

#### On Windows:
- Install **Gpg4win** from [https://gpg4win.org](https://gpg4win.org).

---

## 3. Generating a GPG Key

### Generate a New GPG Key:
```bash
gpg --full-generate-key
```

### Select Options:
- **Key type:** RSA and RSA (default)
- **Key size:** 4096 bits (recommended)
- **Expiration:** Choose a suitable expiry date
- **User Info:** Enter your name and email (must match Git user.email)

### List Available Keys:
```bash
gpg --list-secret-keys --keyid-format=long
```

### Output Example:
```
/Users/username/.gnupg/secring.gpg
------------------------------
sec   4096R/ABCDEF1234567890 2024-02-19 [expires: 2026-02-19]
uid                          Your Name <your_email@example.com>
```

---

## 4. Adding GPG Key to Git

### Copy the GPG Key:
```bash
gpg --armor --export ABCDEF1234567890
```

### Configure Git to Use the Key:
```bash
git config --global user.signingkey ABCDEF1234567890
git config --global commit.gpgsign true
```

> **Tip:** Replace `ABCDEF1234567890` with your key ID.

---

## 5. Adding GPG Key to Git Hosting Services

### 5.1 GitHub:
1. Go to **GitHub > Settings > SSH and GPG keys**.
2. Click **New GPG key**.
3. Paste your GPG public key and save.

### 5.2 GitLab:
1. Go to **GitLab > Preferences > GPG Keys**.
2. Add the key in the provided field.

### 5.3 Bitbucket:
Currently, Bitbucket does not support GPG-signed commits natively.

---

## 6. Verifying Signed Commits

### Make a Signed Commit:
```bash
git commit -S -m "Signed commit message"
```

### Verify Commit Signature:
```bash
git log --show-signature
```

Expected output will show `Good signature from...` if the signing was successful.

---

## 7. Automatically Sign All Commits and Tags

### Sign All Commits:
```bash
git config --global commit.gpgsign true
```

### Sign All Tags:
```bash
git config --global tag.gpgsign true
```

---

## 8. Managing GPG Key Passphrase

### Cache Passphrase Using GPG Agent:
```bash
gpg-agent --daemon
```

On macOS:
```bash
gpg --pinentry-mode loopback --sign
```

> **Tip:** Use tools like GPG Suite (macOS) for passphrase management.

---

## 9. Troubleshooting GPG Signing Issues

### Common Problems & Solutions:

- **GPG Key Not Found by Git:**
  - Ensure the key email matches `git config user.email`.
  - Use `gpgconf --launch gpg-agent` to start the agent.

- **GPG Agent Not Running:**
  - Restart the agent: `gpg-agent --daemon`.

- **Commit Shows as Unverified on GitHub:**
  - Confirm that the GPG key is added to GitHub.
  - Ensure the key ID is correctly set in Git config.

### Debugging GPG:
```bash
gpg --list-keys
gpg --list-secret-keys
```

---

## 10. Best Practices for GPG Key Management

- **Key Expiration:** Set an appropriate expiration and renew as needed.
- **Strong Passphrases:** Protect your private key with a robust passphrase.
- **Backup Keys:** Securely back up GPG keys to avoid losing commit verification capability.
- **Revoke Unused Keys:** Revoke old or compromised keys using:
```bash
gpg --gen-revoke <key-id>
```

---

## 11. Advanced Configurations

### Custom GPG Program Path:
```bash
git config --global gpg.program gpg
```

### Using GPG with Smartcards:
- Set up Smartcard readers for hardware key management.

### Configuring GUI Support:
- Use graphical pinentry programs for passphrase prompts in GUI applications.

---

## Summary

- GPG signing ensures commit authenticity and trust.
- Proper configuration with Git and hosting services allows seamless verification.
- Best practices like key expiration, backups, and passphrase protection improve security.

With GPG signing in place, your Git commit history remains verifiable, secure, and trusted by collaborators and CI/CD pipelines alike.

---

Sign Your Commits, Build Trust! 🛡️✨

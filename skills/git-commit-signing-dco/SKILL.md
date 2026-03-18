---
name: git-commit-signing-dco
description: Enforces Git commit signing with SSH and DCO (Signed-off-by). When suggesting or running git commits, the agent must use -S (sign) and -s (add Signed-off-by). Use when the user asks to commit, when generating commit commands, when amending commits, or when they mention commit signing, DCO, or Signed-off-by.
---

# Git Commit Signing (SSH) and DCO

## Required commit pattern

All commits must be **signed** (`-S`) and include **DCO** (`-s`):

```bash
git commit -S -s -m "Your commit message"
```

- **`-S`** — Sign the commit (SSH or GPG, per repo config).
- **`-s`** — Add `Signed-off-by: Name <email>` (DCO).

Use the same flags when amending: `git commit --amend -S -s --no-edit` or `-m "message"`.

## Before running or suggesting a commit

Signing can **hang** the terminal if the SSH key is not available to Git (e.g. no `ssh-agent` or key not loaded). The user may have to enter a passphrase interactively.

1. **If the agent is about to run `git commit`** (or user asked to commit):
   - Prefer **suggesting** the exact command for the user to run in their terminal (they can enter passphrase if needed), **or**
   - If running the command: first run `ssh-add -l` (or `ssh-add -L`). If it lists keys, signing is likely to succeed without hang. If it exits non-zero or lists nothing, **do not run `git commit`** in the terminal; instead output the command and a short note: "Run this in your terminal. If your SSH key is in the agent, it will sign; otherwise you may be prompted for your passphrase."
2. **When only suggesting** (e.g. "use this command"): always give the full `-S -s` form and optionally add one line: "Ensure `ssh-agent` has your key loaded (`ssh-add -l`) so signing doesn't hang."

## What the agent must do

- **Never** suggest or run `git commit -m "..."` without both `-S` and `-s` (unless the user explicitly asks for an unsigned commit).
- When generating commit messages or commands, always use: `git commit -S -s -m "message"`.
- For amend: `git commit --amend -S -s` (with `--no-edit` or `-m "..."` as appropriate).
- When the user asks "how do I sign commits?" or "set up DCO", point to this pattern and to one-time setup (see reference.md if present).

## Verifying

User can verify signed commits with:

```bash
git log --show-signature -1
```

## One-time setup (reference)

- **SSH signing**: `git config --global gpg.format ssh` and `git config --global user.signingKey /path/to/.ssh/key.pub` (or the key that GitHub/GitLab use).
- **DCO**: `-s` uses `user.name` and `user.email` for the Signed-off-by line; ensure those are set.

For detailed setup and troubleshooting, see [reference.md](reference.md).

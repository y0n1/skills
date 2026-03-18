# Git SSH signing and DCO — setup and troubleshooting

## One-time setup

1. **SSH key for signing** (if not already):
   - Use an existing SSH key or create one. Many setups use `~/.ssh/id_ed25519` / `~/.ssh/id_rsa`.
2. **Tell Git to use SSH for signing**:
   ```bash
   git config --global gpg.format ssh
   git config --global user.signingKey ~/.ssh/id_ed25519.pub
   ```
   Replace with your public key path if different.
3. **DCO**: Signed-off-by comes from:
   ```bash
   git config --global user.name "Your Name"
   git config --global user.email "you@example.com"
   ```
4. **ssh-agent**: Start and add key (e.g. in `.zshrc` / `.bashrc`):
   ```bash
   eval "$(ssh-agent -s)"
   ssh-add ~/.ssh/id_ed25519
   ```

## If `git commit -S` hangs

- Git is waiting for a passphrase (SSH key not in agent or not unlocked).
- Run in another terminal: `ssh-add -l`. If empty, run `ssh-add /path/to/your/key`.
- Or run the commit in a terminal where you can type the passphrase.

## Verify

- List keys in agent: `ssh-add -l`
- Check config: `git config --global --get gpg.format` (should be `ssh`), `git config --global --get user.signingKey`
- Check last commit: `git log --show-signature -1`

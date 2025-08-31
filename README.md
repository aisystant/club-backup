# club-backup

## SSH Key Setup for rsync.net

### 1. Generate SSH Key Pair

Generate a new SSH key pair for rsync.net:

```bash
ssh-keygen -t ed25519 -C "club-backup" -f ~/.ssh/rsync_net_key
```

When prompted for a passphrase, press Enter (no passphrase) to allow automated script usage:
- The private key will be saved as `~/.ssh/rsync_net_key`
- The public key will be saved as `~/.ssh/rsync_net_key.pub`

### 2. Copy Public Key to rsync.net

Use `ssh-copy-id` to copy your public key to the server:

```bash
scp ~/.ssh/rsync_net_key.pub 123@tv-s009.rsync.net:.ssh/authorized_keys
```

Enter your password when prompted. This will automatically add your public key to the server's authorized_keys file.

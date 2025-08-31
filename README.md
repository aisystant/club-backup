# club-backup

## Requirements

Install required packages:

```bash
# Ubuntu/Debian
sudo apt update
sudo apt install sshfs rsync rclone
```

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

## Environment Variables

Copy `.env.example` to `.env` and configure these variables:

```bash
RSYNC_DST=                    # For sql-backup script
SFTP_DST=                     # For sql-backup script
RSYNC_NET_SERVER=             # Username@server for mounting (e.g. 123@tv-s009.rsync.net)
S3_BUCKET=                    # Your S3 bucket name
RSYNC_NET_S3_MOUNTDIR=        # Local mount point (e.g. /mnt/rsync-s3)
RSYNC_NET_S3_SUBDIR=          # Remote directory on rsync.net (e.g. s3-backups)
```

## rclone Configuration

For S3 backup, configure rclone:

```bash
rclone config
```

Create a remote named 's3' with your S3 credentials.

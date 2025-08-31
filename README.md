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
TELEGRAM_BOT_TOKEN=           # Telegram bot token for notifications
TELEGRAM_CHAT_ID=             # Telegram chat ID for notifications
TELEGRAM_MENTIONS=            # Optional: @username mentions for alerts (e.g. "@admin @user")
```

## rclone Configuration

For S3 backup, configure rclone:

```bash
rclone config
```

Create a remote named 's3' with your S3 credentials.

## Telegram Setup

To receive backup notifications via Telegram:

1. Create a Telegram bot:
   - Message @BotFather on Telegram
   - Send `/newbot` and follow instructions
   - Copy the bot token

2. Get your chat ID:
   - Start a chat with your bot
   - Send a message to the bot
   - Visit: `https://api.telegram.org/bot<YOUR_BOT_TOKEN>/getUpdates`
   - Find your chat ID in the response

3. Add the values to your `.env` file:
   ```bash
   TELEGRAM_BOT_TOKEN=your_bot_token_here
   TELEGRAM_CHAT_ID=your_chat_id_here
   ```

## Usage

Test Telegram notifications:
```bash
./send-telegram "Test message"
```

Run S3 backup with notifications:
```bash
./s3-backup
```

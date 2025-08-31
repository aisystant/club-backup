# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a backup system for a Discourse forum with two main backup scripts:
- `s3-backup`: Test script for S3/rsync backup operations
- `sql-backup`: Test script for SQL backup operations with rsync and SFTP support

Both scripts are currently in test/dry-run mode and do not perform actual backup operations.

## Environment Configuration

The scripts depend on environment variables defined in `.env` file:
- `RSYNC_DST`: Destination path for rsync operations
- `SFTP_DST`: Destination path for SFTP operations

Use `.env.example` as a template to create your `.env` file. The `.env` file is gitignored for security.

## Script Architecture

Both backup scripts follow the same pattern:
1. Load environment variables from `.env` file
2. Validate required variables are set
3. Define source and destination paths
4. Execute backup operations (currently in dry-run mode)

The `sql-backup` script includes additional SFTP destination validation and uses `/var/discourse/shared/standalone/backups/` as the source directory for Discourse backups.

## Running Scripts

Execute scripts directly:
```bash
./s3-backup
./sql-backup
```

Both scripts will exit with error code 1 if `.env` file is missing or required variables are not set.
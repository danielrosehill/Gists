---
title: "Local GIthub backups (incremental)"
---

A Bash script for setting up incremental backups of your Github repositories onto a local

## Script

```bash
#!/bin/bash

# Configuration
GITHUB_USERNAME="myusername"
BACKUP_PATH="/backup/here/please"
GITHUB_TOKEN="enter-your-github-pak-here"

# Ensure backup directory exists
mkdir -p "$BACKUP_PATH"

# Fetch all repositories for the user (public and private)
REPOS=$(curl -s -H "Authorization: token $GITHUB_TOKEN" \
    https://api.github.com/user/repos?per_page=100 | jq -r '.[].ssh_url')

# Loop through each repository and perform incremental backup
for REPO in $REPOS; do
    # Extract repository name from SSH URL
    REPO_NAME=$(basename "$REPO" .git)

    # Define local repository path
    LOCAL_REPO_PATH="$BACKUP_PATH/$REPO_NAME"

    if [ -d "$LOCAL_REPO_PATH" ]; then
        # If repository exists locally, fetch updates
        echo "Updating existing repository: $REPO_NAME"
        cd "$LOCAL_REPO_PATH" || exit
        git fetch --all
        git pull origin main || git pull origin master  # Handle both 'main' and 'master' branches
    else
        # If repository does not exist locally, clone it
        echo "Cloning new repository: $REPO_NAME"
        git clone "$REPO" "$LOCAL_REPO_PATH"
    fi
done

echo "Backup completed successfully!"
```
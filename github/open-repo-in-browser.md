---
title: "Open this Github repo in a browser"
---

A small little script that does exactly what it says on the tin:

because:

`git remote -v`

gives you more information than you might need,

this bash script (designed to be attached to a shortcut key) will:

- 1: Just get the repo URL  
- 2: Chop off the `.git` suffix so that you can open it in a browser  
- 3: Open it in a browser

## Use Case

If you've ever wondered: "what's this repository called?" or "is this a private repo?" .... add this to a shortcut and you can find out in a flash!

### Script

```bash
#!/bin/bash

# Extract the repository URL from `git remote -v`
repo_url=$(git remote get-url origin)

# Check if the URL was successfully extracted
if [[ -z "$repo_url" ]]; then
  echo "Error: Could not find a remote repository URL."
  exit 1
fi

# Print the extracted URL
echo "Repository URL: $repo_url"

# Open the URL in Google Chrome (optional)
if command -v google-chrome >/dev/null 2>&1; then
  google-chrome "$repo_url"
else
  echo "Google Chrome is not installed or not in PATH."
fi
```
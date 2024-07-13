+++
title =  "Auto-Commit Unsaved Changes to Isolated Branch Bash Script"
description = "Utility script to commit changes that i have not commited to a branch.. just in case." 
author = "Justin Napolitano"
tags = ["scripting","bash"]
images = ["images/feature-image.png"]
date = "2024-07-13"
categories = ["projects"]
series = ["bash"]
+++

# Auto-Commit and Push Script

This script traverses a specified directory of git repositories, commits all uncommitted changes to a new branch called `auto-commit`, and then pushes the branch to the remote repository. The script includes blacklist functionality to skip specified repositories and checks if the repositories belong to the specified user before committing and pushing changes.

## Prerequisites

- Bash shell
- Git installed
- Proper permissions to access and modify the repositories

## Installation

1. **Create the script**:
   Save the following script to a file named `auto_commit_and_push.sh`:

   ```bash
   #!/bin/bash

   # Define the default root directory where your repos are located
   DEFAULT_ROOT_DIR="/home/cobra/Repos"

   # Define the default blacklist file location
   BLACKLIST_FILE="/etc/auto_commit_blacklist.conf"

   # Define the GitHub username to check against
   GITHUB_USERNAME="your_github_username"

   # Use the provided argument as the root directory, or the default if none is provided
   ROOT_DIR=${1:-$DEFAULT_ROOT_DIR}

   # Export the BLACKLIST_FILE and GITHUB_USERNAME variables so they are available in subshells
   export BLACKLIST_FILE
   export GITHUB_USERNAME

   # Function to check if a repository is blacklisted
   is_blacklisted() {
       local repo_dir=$1
       echo "Checking for Blacklisted $repo_dir in $BLACKLIST_FILE"
       if [ -z "$BLACKLIST_FILE" ]; then
           echo "BLACKLIST_FILE is not set"
           return 1
       fi
       if [ ! -f "$BLACKLIST_FILE" ]; then
           echo "Blacklist file does not exist: $BLACKLIST_FILE"
           return 1
       fi
       grep -qxF "$repo_dir" "$BLACKLIST_FILE"
       local result=$?
       if [ $result -eq 0 ]; then
           echo "$repo_dir is blacklisted"
       else
           echo "$repo_dir is not blacklisted"
       fi
       return $result
   }

   # Function to check if a repository belongs to the specified user
   belongs_to_user() {
       local repo_dir=$1
       local remote_url=$(git -C "$repo_dir" remote get-url origin 2>/dev/null)
       if [[ "$remote_url" == *"$GITHUB_USERNAME"* ]]; then
           return 0
       else
           return 1
       fi
   }

   # Function to commit and push uncommitted changes to auto-commit branch
   auto_commit_and_push() {
       local repo_dir=$1
       echo "Processing repository in $repo_dir"
       cd "$repo_dir" || return

       if is_blacklisted "$repo_dir"; then
           echo "Repository is blacklisted, skipping $repo_dir"
           cd - || return
           return
       fi

       if ! belongs_to_user "$repo_dir"; then
           echo "Repository does not belong to user $GITHUB_USERNAME, skipping $repo_dir"
           cd - || return
           return
       fi

       # Check for uncommitted changes
       if [ -n "$(git status --porcelain)" ]; then
           echo "Uncommitted changes found in $repo_dir"
           
           # Create a new branch auto-commit from the current branch
           git checkout -b auto-commit
           
           # Add all changes to staging
           git add .
           
           # Commit the changes
           git commit -m "Auto commit of uncommitted changes"
           
           # Push the auto-commit branch to the remote
           git push origin auto-commit
           
           echo "Changes have been committed and pushed to auto-commit branch in $repo_dir"
       else
           echo "No uncommitted changes in $repo_dir"
       fi

       cd - || return
   }

   # Export the functions so they can be used by find -exec
   export -f auto_commit_and_push
   export -f is_blacklisted
   export -f belongs_to_user

   echo "Starting auto-commit process for repositories in $ROOT_DIR"

   # Ensure the blacklist file exists
   if [ ! -f "$BLACKLIST_FILE" ]; then
       echo "Blacklist file not found: $BLACKLIST_FILE"
       exit 1
   fi

   # Find all .git directories and commit and push uncommitted changes
   find "$ROOT_DIR" -name ".git" -type d -exec bash -c 'auto_commit_and_push "$(dirname "{}")"' \;

   echo "All repositories processed."
   ```

2. **Make the script executable**:
   ```bash
   chmod +x auto_commit_and_push.sh
   ```

3. **Create the blacklist configuration file**:
   ```bash
   sudo touch /etc/auto_commit_blacklist.conf
   ```

   - Add the paths of the repositories you want to blacklist to this file, one per line. For example:
     ```
     /home/cobra/Repos/repo1
     /home/cobra/Repos/repo2
     ```

4. **Set Your GitHub Username**:
   Replace `your_github_username` in the script with your actual GitHub username.

5. **Run the Script**:
   ```bash
   ./auto_commit_and_push.sh [path_to_repos]
   ```
   - If no path is provided, it defaults to `/home/cobra/Repos`.

## Usage

1. Open a terminal.
2. Run the script by typing:
   ```bash
   ./auto_commit_and_push.sh [path_to_repos]
   ```

   - If no path is provided, it defaults to `/home/cobra/Repos`.

The script will find all `.git` directories in the specified root directory, commit all uncommitted changes to a new branch called `auto-commit`, and push the branch to the remote repository. The script will skip repositories that are blacklisted or do not belong to the specified user.

## License

This project is licensed under the MIT License.

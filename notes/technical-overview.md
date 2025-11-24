---
slug: github-auto-commit-changes-note-technical-overview
id: github-auto-commit-changes-note-technical-overview
title: Auto-Commit Changes
repo: justin-napolitano/auto-commit-changes
githubUrl: https://github.com/justin-napolitano/auto-commit-changes
generatedAt: '2025-11-24T18:31:03.592Z'
source: github-auto
summary: >-
  This repo contains a Bash script that automates the process of committing and
  pushing uncommitted changes across multiple Git repositories. The utility
  creates a branch called `auto-commit` for each repo to keep your changes safe.
tags: []
seoPrimaryKeyword: ''
seoSecondaryKeywords: []
seoOptimized: false
topicFamily: null
topicFamilyConfidence: null
kind: note
entryLayout: note
showInProjects: false
showInNotes: true
showInWriting: false
showInLogs: false
---

This repo contains a Bash script that automates the process of committing and pushing uncommitted changes across multiple Git repositories. The utility creates a branch called `auto-commit` for each repo to keep your changes safe.

### Key Features
- Walks through a directory with multiple Git repos.
- Commits all uncommitted changes to a new `auto-commit` branch.
- Pushes this branch to the remote repository.
- Skips repos on a customizable blacklist.
- Verifies that the user owns the repos before committing.

### Getting Started
1. Save the script as `auto_commit_and_push.sh`.
2. Make it executable:
   ```bash
   chmod +x auto_commit_and_push.sh
   ```
3. Set your GitHub username in the script.
4. Run it, specifying the root directory of your repos (defaults to `/home/cobra/Repos`):
   ```bash
   ./auto_commit_and_push.sh /path/to/your/repos
   ```

*Ensure you have Git and Bash installed.*

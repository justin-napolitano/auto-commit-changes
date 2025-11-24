---
slug: github-auto-commit-changes
id: github-auto-commit-changes
title: Auto-Commit Changes
repo: justin-napolitano/auto-commit-changes
githubUrl: https://github.com/justin-napolitano/auto-commit-changes
generatedAt: '2025-11-24T21:34:00.267Z'
source: github-auto
summary: >-
  A Bash script utility that automates committing and pushing uncommitted
  changes across multiple Git repositories. It creates an isolated branch named
  `auto-commit` for each repo, helping you keep your work safe without manual
  intervention.
tags: []
seoPrimaryKeyword: ''
seoSecondaryKeywords: []
seoOptimized: false
topicFamily: null
topicFamilyConfidence: null
kind: project
entryLayout: project
showInProjects: true
showInNotes: false
showInWriting: false
showInLogs: false
---

A Bash script utility that automates committing and pushing uncommitted changes across multiple Git repositories. It creates an isolated branch named `auto-commit` for each repo, helping you keep your work safe without manual intervention.

---

## Features

- Traverses a specified directory containing multiple Git repositories.
- Automatically commits all uncommitted changes to a new branch called `auto-commit`.
- Pushes the new branch to the remote repository.
- Supports a blacklist to skip specified repositories.
- Verifies repository ownership by GitHub username before committing.

## Tech Stack

- Bash scripting
- Git command-line tools

## Getting Started

### Prerequisites

- Bash shell
- Git installed and configured
- Proper permissions to access and modify the repositories

### Installation

1. Save the script content to a file named `auto_commit_and_push.sh`.
2. Make the script executable:

   ```bash
   chmod +x auto_commit_and_push.sh
   ```
3. (Optional) Create a blacklist file (default path `/etc/auto_commit_blacklist.conf`) listing repositories to skip, one per line.
4. Set your GitHub username in the script by replacing the placeholder `your_github_username`.

### Usage

Run the script with an optional root directory argument where your repositories are located. If no argument is provided, it defaults to `/home/cobra/Repos`.

```bash
./auto_commit_and_push.sh /path/to/your/repos
```

## Project Structure

```
auto-commit-changes/
├── auto-commit-changes.sh  # Main Bash script for auto committing and pushing
├── README.md                # This README file
└── index.md                 # Documentation and blog post metadata
```

## Future Work / Roadmap

- Add support for configurable commit messages.
- Enhance blacklist management with regex or patterns.
- Add logging and reporting features.
- Support for other version control systems.
- Create a Docker container for easier deployment.

---

*This project assumes a Linux environment with Bash and Git installed.*

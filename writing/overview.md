---
slug: github-auto-commit-changes-writing-overview
id: github-auto-commit-changes-writing-overview
title: 'Auto-Commit Changes: A Bash Script for Effortless Git Management'
repo: justin-napolitano/auto-commit-changes
githubUrl: https://github.com/justin-napolitano/auto-commit-changes
generatedAt: '2025-11-24T17:05:31.560Z'
source: github-auto
summary: >-
  I'm always on the lookout for ways to streamline my workflow, especially when
  dealing with multiple Git repositories. That's why I created **Auto-Commit
  Changes**. This nifty Bash script automates the downright tedious task of
  committing and pushing uncommitted changes across various Git repos. Trust me,
  it saves time and keeps my work organized.
tags: []
seoPrimaryKeyword: ''
seoSecondaryKeywords: []
seoOptimized: false
topicFamily: null
topicFamilyConfidence: null
kind: writing
entryLayout: writing
showInProjects: false
showInNotes: false
showInWriting: true
showInLogs: false
---

I'm always on the lookout for ways to streamline my workflow, especially when dealing with multiple Git repositories. That's why I created **Auto-Commit Changes**. This nifty Bash script automates the downright tedious task of committing and pushing uncommitted changes across various Git repos. Trust me, it saves time and keeps my work organized.

## What This Repo Does

**Auto-Commit Changes** takes care of all those uncommitted changes lurking in your directories. It combs through a specified directory, finds all the Git repos, and does the following:

- Creates a new branch named `auto-commit` for each repository.
- Commits all uncommitted changes into that branch.
- Pushes the new branch to the remote repository.

Not only does this eliminate manual intervention, but it also keeps your changes neatly tucked away, just in case you need to revert. Plus, there's a handy blacklist feature that lets you skip repositories you don’t want to mess with. You’re in control.

## Why This Script Exists

Let's be honest: managing multiple repositories can be a pain. I've found myself in situations where I had to manually commit and push changes for various projects, often forgetting one or two along the way. 

I wanted a way to simplify that flow without sacrificing safety. Thus, **Auto-Commit Changes** was born. By automating the commit-and-push routine, I have more brain space for actual development work rather than playing Git hopscotch.

## Key Design Decisions

### Isolated Branches

Using an isolated branch (`auto-commit`) for commits serves a couple of purposes:

- **Safety**: If something goes wrong, I can easily delete that branch without affecting my main work.
- **Organization**: It creates a clear distinction between automatic commits and my intended changes.

### Blacklist Feature

I included a blacklist to prevent the script from touching specific repositories. This feature is essential for keeping things clean and avoiding errors in critical projects. You simply specify repositories to skip, and the script takes care of the rest. 

### Ownership Verification

Before committing, the script checks if you're the owner of the repository based on your GitHub username. This ensures you're not accidentally committing to someone else's work. It's a small but valuable safeguard.

## Tech Stack

The tools I leveraged for this project are pretty straightforward:

- **Bash scripting**: The entire utility is executed through a simple Bash script.
- **Git command-line tools**: I used Git's built-in commands to handle commits and pushes.

Although it’s a minimal stack, the simplicity of Bash coupled with Git’s power does the trick efficiently.

## Getting Started

To get this up and running, you need a couple of prerequisites:

- Bash shell
- Git installed and configured
- Proper permissions to access and modify the repositories

### Installation Steps

1. Save the script content to a file named `auto_commit_and_push.sh`.
2. Make it executable:
   ```bash
   chmod +x auto_commit_and_push.sh
   ```
3. (Optional) Create a blacklist file at `/etc/auto_commit_blacklist.conf`, listing the repositories you want to skip.
4. Set your GitHub username in the script by replacing the placeholder.

### Usage

To use the script, simply run it with an optional argument for the root directory containing your repositories. If you skip the argument, it'll default to `/home/cobra/Repos`.

```bash
./auto_commit_and_push.sh /path/to/your/repos
```

## Future Work / Roadmap

I’m not done here. I’ve got ideas brewing for enhancing this repo:

- **Configurable commit messages**: Give users the option to set custom messages for each commit.
- **Enhanced blacklist management**: Allow regex or patterns for more flexible repository skipping.
- **Logging and reporting**: Add features to log actions taken by the script for troubleshooting.
- **Support for other version control systems**: Let’s face it, Git isn’t the only game in town.
- **Docker container**: Make deployment simpler and more portable.

## Conclusion

With **Auto-Commit Changes**, I'm cutting down on repetitive tasks, allowing me to focus on what really matters: coding and building. If you need a quick way to manage multiple Git repos without getting bogged down in manual commits, give this script a shot.

I share updates and insights about this project (and others) on social platforms like Mastodon, Bluesky, and Twitter/X, so feel free to follow along! 

Check out the repo at [GitHub - auto-commit-changes](https://github.com/justin-napolitano/auto-commit-changes), and let me know what you think. Happy coding!

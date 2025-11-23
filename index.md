---
slug: "github-auto-commit-changes"
title: "auto-commit-changes"
repo: "justin-napolitano/auto-commit-changes"
githubUrl: "https://github.com/justin-napolitano/auto-commit-changes"
generatedAt: "2025-11-23T08:15:06.799494Z"
source: "github-auto"
---


# Auto-Commit Changes: Automating Git Commits Across Multiple Repositories

Hey there! I wanted to share a little utility script I wrote that’s been a real time-saver for me lately. If you’re like me, juggling multiple Git repositories and sometimes forgetting to commit changes before switching contexts, this might resonate with you.

## The Motivation

I often find myself working across a handful of repositories, making quick fixes or experiments, but not always committing those changes right away. It’s easy to lose track or accidentally overwrite work. I wanted a simple way to automatically commit any uncommitted changes across all my repos without manually checking each one.

## What Problem Does This Solve?

The script scans a directory full of Git repositories, checks for any uncommitted changes, and commits those changes to a new branch named `auto-commit`. It then pushes that branch to the remote, so my work is safely backed up even if I haven’t fully polished or merged it yet.

This helps me avoid losing work and keeps my main branches clean until I’m ready to integrate those changes properly.

## How It’s Built

The core is a Bash script leveraging standard Git commands. Here’s a quick overview:

- **Directory traversal:** It takes a root directory as input (or defaults to `/home/cobra/Repos`) and iterates through each subdirectory.
- **Blacklist support:** To avoid committing in certain repos, it supports a blacklist file (`/etc/auto_commit_blacklist.conf`) where repo paths can be listed to skip.
- **Ownership check:** Before committing, it verifies the repository belongs to a specified GitHub username to prevent accidental commits in unrelated repos.
- **Commit and push:** For repos with uncommitted changes, it creates an `auto-commit` branch, commits all changes, and pushes the branch upstream.

## Interesting Implementation Details

- The script exports environment variables like the blacklist file path and GitHub username to subshells for consistent access.
- It uses `grep` to efficiently check blacklist membership.
- The branch creation and push are done programmatically, so no manual Git commands are needed.

## Why this project matters for my career

Automating repetitive tasks like committing changes across multiple repos not only saves time but also reduces human error — a critical skill in any developer’s toolkit. Writing this script sharpened my Bash scripting and Git automation skills, and it’s a practical example I can showcase when discussing automation and workflow optimization in interviews or team discussions. Plus, it reflects my proactive approach to problem-solving and maintaining code hygiene.

---

If you’re interested, feel free to check out the repo and adapt the script to your workflow. Happy coding!
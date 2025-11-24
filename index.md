---
slug: github-auto-commit-changes
title: Bash Script for Auto-Committing Uncommitted Changes Across Git Repos
repo: justin-napolitano/auto-commit-changes
githubUrl: https://github.com/justin-napolitano/auto-commit-changes
generatedAt: '2025-11-23T08:37:27.920638Z'
source: github-auto
summary: >-
  Bash script automating detection, committing, and pushing of uncommitted changes across multiple
  Git repositories with ownership and blacklist controls.
tags:
  - bash
  - git
  - automation
  - shell-script
  - repository-management
seoPrimaryKeyword: auto-commit changes
seoSecondaryKeywords:
  - git automation
  - bash script
  - repository management
seoOptimized: true
topicFamily: automation
topicFamilyConfidence: 1
topicFamilyNotes: >-
  The post specifically focuses on a Bash script to automate git commits across multiple
  repositories, aligning perfectly with the Automation family description and example slugs,
  including the exact slug present.
---

# Auto-Commit Changes: Technical Overview

## Motivation

Managing multiple Git repositories often involves uncommitted changes scattered across projects. Forgetting to commit or push these changes risks data loss or inconsistent states. Manual commits across many repositories are tedious and error-prone.

This script addresses that problem by automating the detection, committing, and pushing of uncommitted changes in multiple repositories under a specified directory. It isolates these commits on a dedicated branch to avoid interfering with ongoing development.

## Problem Statement

- How to efficiently commit uncommitted changes across many Git repositories?
- How to avoid accidental commits to primary branches?
- How to exclude certain repositories from automated commits?
- How to ensure commits are only made to repositories owned by a specific user?

## Implementation Details

The solution is a Bash script that:

1. Defines a root directory containing Git repositories, defaulting to `/home/cobra/Repos`.
2. Uses a blacklist file (`/etc/auto_commit_blacklist.conf`) listing repository paths to skip.
3. Checks each repository under the root directory:
   - Skips if the repository path is blacklisted.
   - Checks if the remote origin URL contains the specified GitHub username to verify ownership.
4. For eligible repositories:
   - Detects uncommitted changes.
   - Creates or switches to an `auto-commit` branch.
   - Adds all changes and commits with a standard message.
   - Pushes the `auto-commit` branch to the remote.

### Blacklist Functionality

The script reads the blacklist file line-by-line and uses exact string matching to determine if a repository should be skipped. This prevents unintended commits to sensitive or irrelevant repositories.

### Ownership Verification

By inspecting the remote origin URL for the GitHub username, the script ensures it only modifies repositories that belong to the intended user. This avoids committing to forks or unrelated repositories.

### Branch Isolation

Using a dedicated `auto-commit` branch prevents interference with main or feature branches. This allows developers to review automated commits separately.

### Limitations and Assumptions

- The script assumes a Unix-like environment with Bash and Git installed.
- The blacklist file must exist and be properly maintained.
- The GitHub username must be correctly set in the script.
- The root directory should contain only Git repositories or directories to be skipped.

## Practical Usage

Run the script periodically or integrate it into workflows to safeguard uncommitted work. It is particularly useful for developers managing multiple projects simultaneously.

## Summary

This script automates a common but overlooked task: committing and pushing uncommitted changes across many repositories safely and efficiently. It balances automation with control via blacklisting and ownership checks, minimizing risks while reducing manual overhead.


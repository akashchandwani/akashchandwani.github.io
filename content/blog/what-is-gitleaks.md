---
title: "What is Gitleaks and How to Use It?"
date: 2022-09-28T23:19:43+05:30
draft: false
tags: ["gitleaks", "git", "security"]
---

**Gitleaks** is an open-source tool designed to detect and prevent secrets (passwords/api-keys) checked into your Git repository. Its main advantage lies in scanning not only your latest source code but also the entire Git history, identifying any secrets committed in the past.

*"Once your secrets are committed, assume it’s leaked."*

*"Use Gitleaks before a hacker uses it to exploit you."*

## How to Use Gitleaks?

Before using Gitleaks, you need to install it. There are various installation options, and we'll cover the best ones based on different scenarios. You can find a list of all available options [here](https://github.com/zricethezav/gitleaks#getting-started).

Here are the most common scenarios where Gitleaks proves useful:

### Scenario 1: Detecting Secrets in Committed Code

If you want to detect secrets committed to your Git source code repository:

1. Install Gitleaks on your system.
    - Mac users: `brew install gitleaks`
    - Windows and Linux users: Download the appropriate version from [here](https://github.com/zricethezav/gitleaks/releases).
2. Open the terminal and navigate to your source code repository: `cd <path-to-your-source-code-repository>`
3. Run the command to find secrets in your Git repository: `gitleaks detect`
4. For detailed information on detected secrets: `gitleaks detect -v`

If you find secrets, consider using tools like BFG Repo Cleaner to remove them.

### Scenario 2: Preventing Secrets from Being Committed

To ensure you don't commit any secrets:

1. Install Gitleaks (refer to Scenario 1).
2. Navigate to your source code repository: `cd <path-to-your-source-code-repository>`
3. Run the command to find secrets in your code changes: `gitleaks protect` (Note: Untracked file secrets are not detected in this step)
4. For detailed information on detected secrets: `gitleaks protect -v`
5. Remove detected secrets.
6. Move code changes to the staging area: `git add <files-to-add-to-staging-environment>` or `git add .`
7. Run the command to find secrets in the staging area: `gitleaks protect --staged`
8. For detailed information on detected secrets in the staging area: `gitleaks protect --staged -v`
9. If secrets are detected, remove them and add the changes back to the staging area.

### Scenario 3: Automating Pre-Commit Checks

Automate the process from Scenario 2 by adding the `gitleaks protect --staged -v` command to your pre-commit hook file.

1. Install Gitleaks (refer to Scenario 1).
2. Navigate to your source code repository: `cd <path-to-your-source-code-repository>`
3. Rename the `pre-commit.sample` file in `.git/hooks` to pre-commit: `mv .git/hooks/pre-commit.sample .git/hooks/pre-commit`
4. Ensure the file has executing permission: `chmod +x .git/hooks/pre-commit`
5. Open the pre-commit file and add: `exec gitleaks protect --staged -v`

You can also use the pre-commit script provided by the Gitleaks community.

### Scenario 4: Team-wide Prevention

To ensure the entire team doesn't check in any secrets:

1. Install pre-commit using the methods [mentioned here](https://pre-commit.com/#installation).
2. Navigate to your source code repository: `cd <path-to-your-source-code-repository>`
3. Create a `.pre-commit-config.yaml`: `touch .pre-commit-config.yaml`
4. Paste the content into the `.pre-commit-config.yaml` file:
    ```yaml {linenos=table,linenostart=1,lineanchors=prefix}
    repos:
    - repo: https://github.com/zricethezav/gitleaks
        rev: v8.11.2
        hooks:
        - id: gitleaks
    ```
5. Update Gitleaks version: `pre-commit autoupdate`
6. Install pre-commit: `pre-commit install`
7. When committing, the pre-commit hook checks for secrets. Make sure each developer installs pre-commit using steps 1 and 6.

### Scenario 5: CI Integration

Scan the project whenever anyone pushes code to the repository using `gitleaks detect` in CI tools like Github Actions.

### Scenario 6: Using Gitleaks with Non-Git Repositories

Gitleaks can be used with any source code repository, even if not version-controlled by Git. Use Gitleaks with a non-Git repository: `gitleaks detect --no-git`

## Conclusion

This blog covers various scenarios on how to use Gitleaks to detect and protect your source code from accidental leaks. The next blog will delve into how to remove detected secrets from your source code repository.

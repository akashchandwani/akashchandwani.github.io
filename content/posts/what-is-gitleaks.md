---
title: "What is Gitleaks and how to use it?"
date: 2022-09-28T23:19:43+05:30
draft: true
---

Gitleaks is an open source tool used to detect and prevent secrets (passwords / api-keys) checked-in to your git repository. The main advantage of Gitleaks is that it not only scans your latest source code but also the entire git history identifying any secrets committed to your source code in the past as well.

"Once your secrets are committed, assume it’s leaked."

"Use gitleaks before a hacker uses it to exploit you…" — Your friend at open source

# How to use Gitleaks?

Before you can use Gitleaks, you will need to install it. There are several ways to install it. We will cover the best installation option according to the scenarios discussed below. Here is a list of all available options if you want to visit it now.

There are several scenarios where you would find Gitleaks useful. I have listed down the most common scenarios below:

# Scenario 1:

Everything is committed in my git source code repository and I want to find if there are/were any secrets committed.

This is the most common scenario if you want to detect any secrets committed to your git source code repository. For this, you can:

1. Install gitleaks on your system.
2. Mac users can install gitleaks via homebrew using the command — brew install gitleaks .
3. Windows and Linux users can visit the release page of Gitleaks here and download and install the appropriate version from there.
4. Open terminal and go to the source code repository you want to detect secrets from. cd <path-to-your-source-code-repository>
5. Run the following command to find if there are secrets committed in your git repository — gitleaks detect .
6. Run the following command to find the details of secrets committed in your git repository — gitleaks detect -v

If you have found some secrets in your source code repository and you want to erase them, there are several tools that can help you. BFG repo cleaner is one of them. I will be soon writing a separate blog on how to use this tool…

# Scenario 2:

I want to make sure that I don’t commit any secret in my git source code repository

There is a famous saying — “Prevention is better than cure”. Similarly it’s better to protect your repository from accidental leaks rather than cleaning it later. For this, you can:

1. Install gitleaks on your system. (Refer step 1 in scenario 1)
2. Open terminal and go to the source code repository you want to inspect for any secrets. cd <path-to-your-source-code-repository>
3. Run the following command to find any secrets in your code changes — gitleaks protect . (Note: Secrets in untracked files are not detected in this step)
4. Run the following command to find the details the secrets in your code changes— gitleaks protect -v
5. Remove any secrets that were detected in step 3 and step 4.
6. Move your code changes to staging area by using the command — git add <files-to-add-to-staging-environment> .
7. Use git add . to move all code changes to the staging area.
8. Run the following command to find if there are any secrets in the staging area in your git repository — gitleaks protect --staged
9. Run the following command to find the details if there are secrets in the staging area — gitleaks protect --staged -v
10. If there were any secrets detected in step 7 and step 8. Remove the secrets and add the changes back to the staging area.

# Scenario 3:

I want to automate the process of checking secret in my code changes in before I commit it

In this scenario, what we want to automate the process mentioned in scenario 2. As a human we are prone to making mistakes, and sometimes we might forget to check if we are adding secrets in our commits. For this, we can add gitleaks protect --staged -v command in our pre-commit hook file. Follow the steps:

1. Install gitleaks in your system. (Refer step 1 in scenario 1)
2. Open terminal and go to the source code repository you want to inspect for any secrets. cd <path-to-your-source-code-repository>
3. Rename the pre-commit.sample file in your .git/hooks folder to pre-commit using the command —
    mv .git/hooks/pre-commit.sample .git/hooks/pre-commit
4. Make sure the file has executing permission by running the following command —
5. chmod +x .git/hooks/pre-commit
6. Open the pre-commit file in your preferred editor and add the following line at the end of the file —
    exec gitleaks protect --staged -v

Instead of step 5, you can also choose to use the pre-commit script provided by the gitleaks community. For this, replace the content in your pre-commit file with the content with this.
# Scenario 4:

I want to make sure that my team does not check-in any secret in the source code repository

In the previous scenario we have automated the process of detecting secrets before it’s checked-in in your local repository. But in a more real scenario, a team works on the same source code repository and managing git-hooks in each of the individual’s machine could be cumbersome and manual process. For this, we can use a pre-commit tool for managing this configuration across developer’s machine. The steps for it are:

1. Install pre-commit using one of the following ways mentioned here.
2. Open terminal and go to the source code repository you want to inspect for any secrets. cd <path-to-your-source-code-repository>
3. Create a .pre-commit-config.yaml . Mac and linux users can use touch command for it— touch .pre-commit-config.yaml
4. Add the content into the file from here or from the code in code reference section below.
5. Update the version of gitleaks in the file using the following command — pre-commit autoupdate
6. Install the pre-commit in your pre-commit hooks using the following command — pre-commit install
7. Now when ever you commit, the pre-commit hook installed in your repository will check if any secrets are present in your changes. You will just need to make sure every of developer installs pre-commit using the step 1 and installs pre-commit using the command in step 7.

Code Reference:
pre-commit-config.yml file used in step 4.
.pre-commit-config.yml file (https://gist.github.com/akashchandwani/4665bb3e211fed6197eb048ce756886a)

# Scenario 5:

What if my team mate does not update his/her pre-commit hook file and checks-in a secret

Well, mistakes can happen from anyone. Also, you can’t make sure if every developer in your team has updated his/her pre-commit config. They can be ignorant and not follow the steps. The best way to make sure that secrets are not checked-in is at the entry point of your remote source code repository i.e., to scan the project once anyone pushes the code to the source code repository. This can be achieved by running gitleaks detect command in your remote source code repository when ever a code is checked into the repository. This can be configured via various CI tools.

If your remote source code is in Github and you use Github Actions for your CI process, you can use gitleaks in Github Actions to detect any leaks from your repository.
# Scenario 6:

I don’t use git, can I still use gitleaks to detect secrets in my source code?

Yes absolutely. You can use Gitleaks with any source code repository even if it’s not version controlled by git. To use gitleaks with non-git repository, use gitleaks detect with --no-git option.

1. Install Gitleaks on your system (Refer step 1 in scenario 1)
2. Run gitleaks detect command with --no-git option —
    gitleaks detect --no-git

# Conclusion:

In this blog we have seen various scenarios on how to we can use gitleaks to detect and protect our source code from accidental leaks. In my next blog I will write on how to remove secrets from your source code repository if you have detected it. Don’t forget to follow to stay updated… :)
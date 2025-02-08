+++
title = "Git Commands"
image = "/images/post/gitcommands.jpg"
author = "Sedat"
date = "2025-02-08T00:05:00Z"
description = "git commands"
categories = ["Git"]
type = "post"

+++
Git provides a variety of useful commands that streamline version control and collaboration. The git init command initializes a new repository, while git clone <repo_url> copies an existing repository to your local machine. To track changes, you can use git add <file> to stage files and git commit -m "message" to save changes with a message. The git status command helps check the repository's state, and git log displays commit history. To synchronize with a remote repository, git push uploads local changes, while git pull fetches and merges updates from the remote. If you need to switch branches, git checkout <branch> or git switch <branch> is useful, and git merge <branch> combines changes from another branch. For undoing changes, git reset and git revert allow rolling back commits safely. These commands form the foundation for efficient Git workflows.

***

##### Github Ubuntu CLI Configuration

```
(check version)
git --version

(configure git user mail)
git config --global user.email "mail@example.com"

(configure git user)
git config --global user.name "github-username"

(list configuration made
git config --list

(install github cli tool)
sudo apt install gh

(login)
gh auth login

(give access to delete repo)
gh auth refresh -h github.com -s delete_repo
```

***

##### Return to specific commit

```
git log --pretty=format:"%h - %an, %ar : %s"
git reset --hard 9f08cd6
git add -A && git commit -am "test"
git push --force
```

***

##### Create repository

```
gh repo create link --private
nano README.md

git init
git add .
git commit -m "first-commit"

git remote add origin https://github.com/github-username/test-project.git   (you can find here: git remote -v)

git branch -M main
git push -u origin main
```

***

##### Delete repository

```
gh repo delete test-project
rm -rf .git
```

***

##### List repository

`gh repo list github-username --visibility=private`

***

##### Clone repository

```
gh repo clone test-repo
or
gh repo clone github-user/test-repo
```

***

##### Add all file and folders in current directory, commit and apply changes

```
git add .
git commit -m "first-commit"
git fetch (or git push for local changes)
```

***

##### After commit see changes before push

`git diff`

***

##### List commit history

```
git log
or
git log --graph --oneline --all
```

***

##### Create new branch

`git checkout -b my-feature-branch`

***

##### Return to main branch

`git checkout main`

***

##### List all branches

`git branch -a`

***

##### Push changes to new branch

```
git push origin my-feature-branch

if not set upstream branch use this:
git push --set-upstream origin my-feature-branch
```

***

##### To keep things tidy, you can delete the feature branch locally

`git branch -D my-feature-branch`

***

##### If you’ve pushed your feature branch to a remote repository (like GitHub), you can also delete it there

`git push origin --delete my-feature-branch`

***

##### Merging Changes (Optional, when you want to apply a branch to main branch), When your feature is complete, merge it back into the main branch

```
git checkout main
git merge my-feature-branch
git push
```

***

##### Create new branch from commit

```
git checkout -b my-new-branch 797bd45

(or you can switch to commit using hash only)
git checkout <commit-hash>
```

***

##### To discard all local changes and get the current branch from the remote repository using Git, you can follow these steps

```
git checkout main
git fetch
git reset --hard origin/main
git clean -fd
```

***

##### Change last commit message

`git commit --amend`

***

##### Undo most recent commit and keep changes

`git reset HEAD~1`

***

##### Undo the N most recent commit and keep changes

`git reset HEAD~N`

***

##### Undo most recent commit and get rid of changes

`git reset HEAD~1 --hard`

***

##### Reset branch to remote state

```
git fetch origin
git reset --hard origin/[branch-name]
```

***

##### Renaming the local master branch to main

`git branch -m master main`

***

##### Git periodically performs garbage collection to clean up unreachable objects. You can manually trigger it with

`git gc`

***

##### Pull Requests using CLI (we (collobrators) use pull requests to merge our code to the specific(main usually) branch)

```
(collobrator)
gh pr create --base main --head test1 --title "mypull request"

(admin)
gh pr list
gh pr merge --admin 4


To see closed PRs:
gh pr list --state all

To search for specific PRs using a query (similar to GitHub’s search syntax):
gh pr list --search "status:success review:required"
```

***

##### When it comes to reviewing and confirming changes using the command line interface (CLI), you have a few options depending on the Git platform you’re using. Let’s explore how you can achieve this

```
GitHub

If you’re working with GitHub, you can use the following steps to review and merge changes via the CLI:
First, ensure you have the latest changes from the main branch:
git checkout main
git pull origin main

Next, create a new branch for your changes (if you haven’t already):
git checkout -b my-feature-branch

Make your changes, commit them, and push to your branch:
git add .
git commit -m "My changes"
git push origin my-feature-branch

Now, create a pull request (PR) using the GitHub CLI:
gh pr create --base main --head my-feature-branch --title "My Pull Request"

Review the PR on GitHub, discuss any necessary changes, and approve it.
Finally, merge the PR:
gh pr merge <PR_NUMBER>


GitLab

For GitLab, you can follow similar steps:
Create a new branch, make changes, and commit them.
Push your branch to GitLab:
git push origin my-feature-branch

Create a merge request (MR) using the GitLab CLI:
gitlab mr create --source=my-feature-branch --target=main --title="My Merge Request"

Review the MR on GitLab, discuss changes, and approve it.
Merge the MR:
gitlab mr merge <MR_ID>


Bitbucket

Bitbucket also supports similar workflows:
Create a branch, make changes, and commit them.
Push your branch to Bitbucket:
git push origin my-feature-branch

Create a pull request using the Bitbucket CLI:
bitbucket pr create --source=my-feature-branch --destination=main --title="My Pull Request"

Review the PR on Bitbucket, discuss changes, and approve it.
Merge the PR:
bitbucket pr merge <PR_ID>
```

* Remember to replace placeholders like <PR_NUMBER>, <MR_ID>, and branch names with actual values from your repository. And hey, reviewing code via CLI is like being a code detective—examining every line for clues! 🕵️‍♂️🔍


***

##### If you have issue pushing unwanted file and folders reason of .gitignore missing configuration (like node_modules not listed), you can clean these from remote and local

```
(if you are already in mian branch and you can push this)
echo "node_modules/" >> .gitignore
git add .gitignore
git commit -m "Add node_modules to .gitignore"


Verify the largest files/objects in the repository Sometimes large files might still exist in the history. You can check the largest objects in your Git repository using:

git rev-list --objects --all | sort -k 2 > allfiles.txt

(we need this tool, install using python3 pip)
pip install git-filter-repo


echo "node_modules/" >> .gitignore

echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc

git filter-repo --path node_modules --invert-paths --force

git remote add origin https://github.com/github-username/test-project.git

git push origin main --force

git checkout main

git push --set-upstream origin main

com test

git push

(optional)
git pull origin main --rebase
```

***

### Clone specific directory of the repository example


First, clone the entire repository but with a filter to minimize the data downloaded:

`git clone --filter=blob:none --no-checkout https://github.com/test/test-project.git`

Navigate into the Repository: Change into the cloned repository directory:

`cd test-project`

Enable Sparse Checkout: Enable sparse checkout to specify which directories you want:

`git sparse-checkout init --cone`

Specify the Directory: Add the specific directory you want to check out:

`git sparse-checkout set plugins/logo`

Checkout the Files: Finally, checkout the files in that directory:

`git checkout master`

* This process allows you to clone only the specific directory you need without downloading the entire repository history.

***

##### When it comes to reviewing and confirming changes using the command line interface (CLI), you have a few options depending on the Git platform you’re using. Let’s explore how you can achieve this

```
GitHub

If you’re working with GitHub, you can use the following steps to review and merge changes via the CLI:
First, ensure you have the latest changes from the main branch:
git checkout main
git pull origin main

Next, create a new branch for your changes (if you haven’t already):
git checkout -b my-feature-branch

Make your changes, commit them, and push to your branch:
git add .
git commit -m "My changes"
git push origin my-feature-branch

Now, create a pull request (PR) using the GitHub CLI:
gh pr create --base main --head my-feature-branch --title "My Pull Request"

Review the PR on GitHub, discuss any necessary changes, and approve it.
Finally, merge the PR:
gh pr merge <PR_NUMBER>


GitLab

For GitLab, you can follow similar steps:
Create a new branch, make changes, and commit them.
Push your branch to GitLab:
git push origin my-feature-branch

Create a merge request (MR) using the GitLab CLI:
gitlab mr create --source=my-feature-branch --target=main --title="My Merge Request"

Review the MR on GitLab, discuss changes, and approve it.
Merge the MR:
gitlab mr merge <MR_ID>


Bitbucket

Bitbucket also supports similar workflows:
Create a branch, make changes, and commit them.
Push your branch to Bitbucket:
git push origin my-feature-branch

Create a pull request using the Bitbucket CLI:
bitbucket pr create --source=my-feature-branch --destination=main --title="My Pull Request"

Review the PR on Bitbucket, discuss changes, and approve it.
Merge the PR:
bitbucket pr merge <PR_ID>
```

* Remember to replace placeholders like <PR_NUMBER>, <MR_ID>, and branch names with actual values from your repository. And hey, reviewing code via CLI is like being a code detective—examining every line for clues! 🕵️‍♂️🔍


***

### Git Branch Strategies

Ah, the delightful world of Git branching strategies! Choosing the right one can feel like picking the perfect ice cream flavor—so many options, and they all have their unique appeal. Let’s explore some popular Git branching strategies, shall we? 🍦🌿

#### GitHub Flow

For Continuous Deployment and Simplicity

##### How It Works

Main branch (often main or master) is always deployable.
Feature branches are short-lived and created for specific tasks.
Pull Requests (PRs) are used for code review and merging.

##### When to Use It

Ideal for small teams and continuous deployment.
Keeps things simple and straightforward.

#### GitFlow

For Complex Release Workflows

##### How It Works

Main branches: main (production-ready) and develop (ongoing development).
Feature branches for new features.
Release branches for preparing releases.
Hotfix branches for emergency fixes.

##### When to Use It

Larger teams with complex release schedules.
Ensures a structured workflow.

#### Trunk Based Development

For High Development Velocity

##### How It Works

Main branch (trunk) is always deployable.
Feature branches are short-lived.
Frequent integrations into the main branch.

##### When to Use It

Fast-paced development environments.
Minimizes long-lived branches.

* Remember, there’s no one-size-fits-all answer. Choose the strategy that aligns best with your team’s needs, workflow preferences, and deployment schedules.

***

### Essential Git Flow commands - how to do using git

#### Creating a Feature Branch:

##### Git Flow

`git flow feature start <name>`

##### Git

`git checkout -b feature/my-awesome-feature`

#### Finishing a Feature Branch

##### Git Flow

`git flow feature finish <name>`

##### Git

```
git checkout develop
git merge feature/my-awesome-feature
```

#### Starting a Release

##### Git Flow

`git flow release start <version>`

##### Git (assuming you're on develop)

`git checkout -b release/1.0.0`

#### Finishing a Release

##### Git Flow

`git flow release finish <version>`

##### Git

```
git checkout main
git merge release/1.0.0
git checkout develop
git merge release/1.0.0
```

#### Creating a Hotfix Branch

##### Git Flow

`git flow hotfix start <name>`

##### Git

`git checkout -b hotfix/fix-that-bug`

#### Finishing a Hotfix

##### Git Flow

`git flow hotfix finish <name>`

##### Git

```
git checkout main
git merge hotfix/fix-that-bug
git checkout develop
git merge hotfix/fix-that-bug
```

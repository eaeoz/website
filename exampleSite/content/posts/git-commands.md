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

##### Github Ubuntu CLI Configuration:

```
(check version)
git --version

(configure git user mail)
git config --global user.email "sedatergoz@gmail.com"

(configure git user)
git config --global user.name "eaeoz"

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

### Return to specific commit:

```
git log --pretty=format:"%h - %an, %ar : %s"
git reset --hard 9f08cd6
git add -A && git commit -am "test"
git push --force
```

***

### Create repo:

```
gh repo create link --private
nano README.md

git init
git add .
git commit -m "first-commit"

git remote add origin https://github.com/eaeoz/test-project.git   (you can find here: git remote -v)

git branch -M main
git push -u origin main
```

***

### Delete repo:

```
gh repo delete test-project
rm -rf .git
```

***

### List repo:

`gh repo list github-username --visibility=private`

***

### To keep things tidy, you can delete the feature branch locally:

`git branch -D my-feature-branch`

***

### If you’ve pushed your feature branch to a remote repository (like GitHub), you can also delete it there:

`git push origin --delete my-feature-branch`

***

### Git periodically performs garbage collection to clean up unreachable objects. You can manually trigger it with:

`git gc`

***

### Pull Requests using CLI (we (collobrators) use pull requests to merge our code to the specific(main usually) branch):

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

### Clone specific directory of the repository example:


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

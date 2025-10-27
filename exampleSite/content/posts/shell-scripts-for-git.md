+++
title = "Shell Scripts For Git"
image = "/images/post/github.jpg"
author = "Sedat"
date = "2025-10-24T00:03:01Z"
description = "shell scripts for git"
categories = ["Git"]
type = "post"

+++

Using a GitHub shell script to add configurations to .bashrc offers several benefits. It automates the process, ensuring consistency across different environments without manual editing. This is particularly useful for setting up aliases, environment variables, and custom functions quickly. By storing the script in a repository, you can track changes, roll back modifications if needed, and easily share configurations with others. Additionally, the script can be executed on multiple machines, streamlining setup for developers who work across different systems.

***

#### Commit Changes

##### Usage:

```
com testcommit
```

##### Code:

```
com() {
    git add -A && git commit -am "$1"
}
```

***

#### Commit with message and Push at the same time

##### Usage:

```
push "commitmessage"
```

##### Code:

```
push() {
    local branch_name
    branch_name=$(git rev-parse --abbrev-ref HEAD 2> /dev/null)
    if [ -n "$branch_name" ]; then
        git add -A && git commit -am "$1" && git push origin "$branch_name"
    else
        echo "Not on any branch (detached HEAD state)"
    fi
}
```

***

#### Create New Project

##### Usage:

```
new testproject
```

##### Code:

```
new() {
    # Initialize Git repository
    git init
    # Create README.md file
    echo "# $1" > README.md
    # Stage all files and make initial commit
    git add . && git commit -m "Initial commit"
    # Create GitHub repository
    gh repo create "$1" --private --source . --remote origin
    # Short pause
    sleep 2
    # Ensure branch is named 'main' and push to GitHub
    git branch -M main
    git push -u origin main
    echo "Repository '$1' created and initialized successfully!"
}
```

***

#### List Commit History

#### Usage:

```
log
```

#### Code:

```
log() {
    git log --pretty=format:"%h - %an, %ar : %s"
}
```

***

#### Pull Request

##### Usage:

```
req main test pullrequestcomment
```

##### Code:

```
req() {
    # Extract the arguments
    base_branch="$1"
    head_branch="$2"
    pr_title="$3"

    # Replace placeholders in the command
    command="gh pr create --base $base_branch --head $head_branch --title \"$pr_title\""

    # Execute the command
    eval "$command"
}
```

***

#### Return to Last Changes For Current Branch

##### Usage:

```
clean
```

##### Code:

```
clean() {
    current_branch=$(git rev-parse --abbrev-ref HEAD)
    git checkout "$current_branch"
    git fetch
    git reset --hard "origin/$current_branch"
    git clean -fd
}
```

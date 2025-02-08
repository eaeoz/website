+++
title = "Shell Scripts for Git"
<!-- image = "/images/post/post-1.jpg" -->
author = "Sedat"
date = "2025-02-08T00:01:00Z"
description = "shell scripts for git"
categories = ["Git"]
type = "post"

+++
## Shell Scripts for Git

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

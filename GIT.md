# Quick Git


A quick overview of the main commands for working with the Git version control system.

## Content

-   [Basic commands](#basic-commands)
-   [Information about commits](#information-about-commits)
-   [Working with branches](#working-with-branches)
-   [Remote repositories](#remote-repositories)
-   [Deferred (hidden) commits](#deferred-hidden-commits)
-   [Commit deletions and rollbacks](#commit-deletions-and-rollbacks)
-   [Additional and similar resources](#additional-and-similar-resources)

## Basic commands

A **repository** is a place where the source code and change history of your project is stored. A repository can be local (on your computer) or remote (on a server).

```shell
git init # Initializing a new repository
```

```shell
git status # Show the status of files in the current repository
```

-   **Untracked files** - Git doesn't know these files exist, so it has no effect on them.
-   **Modified files** - these files were previously added for tracking and now Git has detected that their contents have changed since the last commit.
-   **Files in Index (Staged)** is the intermediate state of files that were previously Untracked or Modified and are now pre-committed and ready to be included in a new commit.

```shell
git add . # Add all Untracked and Modified files in Index
git add file.name # Add only a specific file
git add ./**/*.js # Add all files with the .js extension
```

```shell
git rm file.name # Remove the added file from Index
git reset file.name # Similar to the command above
```

**Commit** is a record in the repository history that represents information about changes to files. Each commit has a unique identifier (hash) and some metadata.

```shell
git commit -m "comment" # Create a new commit with the specified message
git commit --amend -m "Updated message" # Overwrite the message for the last commit
git commit --amend --no-edit # Add changes to the last commit
```

```shell
git tag <tag_name> <commit_hash> # Add a tag (alias) for the commit.
# This tag can now be used instead of a hash to refer to a specific commit.
git tag # Display a list of available tags
```

```shell
git mv <path/to/file> <new/path/to/file> # Moving a file (a special case of renaming)
```

```shell
git restore file.name # Canceling changes to a file that has not yet been committed
git checkout file.name # Similar to the command above (obsolete approach)
```

## Information about commits

```shell
git log # Display commit history
git log -3 # Output the last 3 commits
git log --oneline # History output in one line for each commit
git reflog # Information about commits and actions performed (stored locally for you only)
```

```shell
git show <commit_hash> # Show commit information
git diff <commit_hash> # Show the difference between the selected commit and the current state
git diff <commit_hash> <commit_hash> # Show the difference between two commits
git diff <file_name> # Show changes to the selected file
```

## Working with branches

**Branch** - a sequence of commits. As a rule, there is one main branch (Master/Main branch) in a repository. From this branch (from any of its commits) you can start new independent branches, where you can develop some new functionality, adding more and more new commits.

```shell
git branch # Display a list of available branches and the current branch
git checkout -b <branch_name> # Create a new branch from the current one and go directly to it
git checkout - # Quickly switch to the previous branch
git branch <branch_name> # Switch to another branch
git branch <new_branch_name> <commit_hash> # Create a branch from a specific commit
```

**Merge** - the process of joining changes from one branch into another.

```bash
git merge <branch_name> # Merge the current branch with the specified branch (with all its commits)
git merge --squash <branch_name> # Similar to the command above, only all commits will be merged into one final one
git cherry-pick <commit_hash> # Merge the current branch with a commit from another branch
git rebase <branch_name> # Update commit history and integrate changes from the specified branch
git branch -d <branch_name> # Delete branch
```

**Merge conflict** - a merge situation where two branches have different changes in the same location and Git cannot automatically merge them.

## Remote repositories

```shell
git remote add origin <URL> # Connect to the remote repository and name it "origin"
git push --set-upstream origin <branch_name> # Connect the branch to "origin" repo
git push # Send changes to a remote repository
git pull # Download changes from a remote repository and immediately merge to the local branch
git fetch # Only download changes from a remote repository without automatic merge
# (this will allow you to view the code and decide for yourself how to merge it with local)
git push -u origin <branch_name> # Send a new branch to a remote repository
git push --delete origin <branch_name> # Remove a branch from a remote repository
git remote remove origin # Remove connection to remote "origin" repository
git remote -v # Show the list of connected remote repositories
```

## Deferred (hidden) commits

**Git stash** allows you to temporarily save ongoing uncommitted changes in a special area called `stash`. This is useful when you want to switch to another task or branch, but don't want to commit incomplete changes. You can later apply the saved changes back to your working copy.

```shell
git stash save "message" # Save the currently changes to stash with the specified message
git stash list # View a list of all saved stashes
git stash apply # Retrieve the last saved changes from stash, leaving a copy in stash
git stash apply <stash_number> # Retrieve saved changes from stash by its sequence number, leaving a copy in stash
git stash pop # Retrieve the last saved changes from stash and delete their copy from stash
git stash clear # Clear stash
```

## Commit deletions and rollbacks

```bash
git reset <commit_hash> # Delete all commit commits up to the specified commit
# All changes from deleted commits can now be committed again
# (e.g., to create a single shared commit)
git reset --hard # Delete all uncommitted changes and modifications added to the index but not yet committed
git revert <commit_hash> # Create a new commit that undoes changes made to the specified commit
# (a secure way to roll back changes while retaining all history)
```

## Additional and similar resources

-   [**Learn Git concepts, not commands** - GitHub](https://github.com/UnseenWizzard/git_training)
-   [**Understanding Git through images** - DEV Community](https://dev.to/nopenoshishi/understanding-git-through-images-4an1#adapt-to-remote)
-   [**A curated list of Git tools, resources and shiny things** - GitHub](https://github.com/dictcp/awesome-git)
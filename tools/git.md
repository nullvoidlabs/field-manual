# tools/git.md

## Initialize and clone repositories
    git init [directory]                         # create a new repo locally
    git clone <url>                              # clone a remote repo

## Configuration
    git config user.name "<name>"
    git config user.email "<email>"
    git config --global color.ui auto            # enable colored output
    git config --global alias.<name> <command>   # create an alias

## Staging and snapshot
    git status                                   # show working directory status
    git add <file>                               # stage a file
    git add .                                    # stage all changes
    git reset <file>                             # unstage a file
    git diff                                      # show unstaged changes
    git diff --staged                             # show staged changes

## Committing
    git commit -m "<message>"                    # commit staged changes
    git commit -am "<message>"                   # stage & commit tracked files

## Branching and switching
    git branch                                   # list branches
    git branch -a                                # list all (including remote)
    git branch <name>                             # create branch
    git switch <name> OR git checkout <name>      # switch branch
    git switch -c <name> OR git checkout -b <name> # create & switch
    git branch -d <name>                         # delete branch
    git branch -D <name>                         # force-delete

## History inspection
    git log                                      # show commit history
    git log --oneline                             # succinct history
    git show <commit>                             # show a commit
    git log <file>                                # history for a file

## Differences
    git diff HEAD                                # diff with HEAD
    git diff <commit>                             # diff with commit
    git diff <commit1> <commit2>                  # diff between commits

## Undo and recovery
    git restore <file>                            # discard unstaged changes
    git restore --staged <file>                   # unstage without discarding
    git reset --hard <commit>                     # reset to commit (dangerous)
    git clean -f                                  # remove untracked files
    git stash                                     # stash changes
    git stash pop                                 # reapply stashed changes
    git revert <commit>                           # create a commit that undoes another

## Remote repositories
    git remote add <name> <url>                   # add remote
    git fetch <remote>                            # fetch changes
    git pull                                       # fetch + merge
    git pull --rebase                              # fetch + rebase
    git push                                       # push current branch
    git push -u <remote> <branch>                # set upstream
    git push --force-with-lease                   # safer force push
    git push --tags                               # push all tags

## Branch integration
    git merge <branch>                            # merge into current branch
    git rebase <branch>                           # reapply commits onto branch
    git cherry-pick <commit>                      # apply single commit

## Tags
    git tag <name>                                # add a tag
    git tag -d <name>                             # delete tag

## Restore specific files
    git checkout <commit> -- <file>               # restore file from commit
    git restore --source <commit> <file>          # equivalent restore

## Useful inspection commands
    git log --follow <file>                       # history including renames
    git log --stat                                # show stats per commit
    git blame <file>                              # show last change per line

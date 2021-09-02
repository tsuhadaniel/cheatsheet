## Git

Configuration
```
git config --global user.name "[name]"
git config --global user.email "[email address]"
git config --global core.editor "nano"
git config --global color.ui true
```

Initialize a repositpory
```
git init
git init --bare (Server)
```

Clone a repository
```
git clone git@github.com:tsuhadaniel/cheatsheet.git
git clone https://github.com/tsuhadaniel/cheatsheet.git
```

Show modified files
```
git status
```

Undo changes
```
git checkout -- [file] (before add)
git reset HEAD [file] (after add)
git revert [hash] (after commit)
```

Add files to staging
```
git add [file]
git add --all
```

Commit
```
git commit -m "[message]"
git commit --amend -m "[message]"
git commit --amend --no-edit
```

Undo commit
```
git reset --soft HEAD^
```

Reset staging area
```
git reset
```

Reset staging area and overwrites all changes
```
git reset --hard
```

Go to/Create a branch
```
git branch [branch name] (create)
git checkout -b [branch name] (create and go)
```

Update branch
```
git pull
git pull [remote branch] [local branch]
```

Delete branch
```
git branch -D [branch]
```

Rename branch
```
git branch -m [new branch name]
```

Update local repository
```
git pull --rebase origin master
```

Edit log
```
git rebase -i [HEAD~n|hash]
```

Update remote branch
```
git push [remote (origin)] [branch]
```

Add remote server
```
git remote add [remote (origin)] git@github.com:tsuhadaniel/cheatsheet.git
```

Log
```
git log
git log --oneline
git log --graph
git log -p
```

Stash
```
git stash
git stash pop
```

Tag
```
git tag -a [tag]
git push origin [tag]
```

Binary Search
```
git bisect [help|start|bad|good|new|old|terms|skip|next|reset|visualize|view|replay|log|run]
```

## Git

Configuration
```
git config --global user.name "[name]"
git config --global user.email "[email address]"
git config --global color.ui true
```

Initialize a local repositpory
```
git init
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
git checkout [branch name]
```

Update branch
```
git pull
git pull [remote branch] [local branch]
```

Delete branch
```
git branch -d [branch name]
```

Update local repository
```
git pull --rebase origin master
```

Update remote branch
```
git push origin 
```

Add remote server
```
git remote add origin git@github.com:tsuhadaniel/cheatsheet.git
```

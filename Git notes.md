Git notes
----------
Some notes on how to set up and use git, specifically geared towards github.

### Setup
#### Config
```
git config --global user.name
git config --global user.email example@email.com
```
The first line will check what username is currently set to git. The second line will **set** the git email to example@email.com. The `--global` flag is used to set the user for all git projects owned by the computers user (`--system` will set it for other users using the same computer as well). `--local` will set the user only for the current repository.

```
git config --global color.ui true
```

It is recommended to set the color.ui variable to true, since it will colour some words in the git output appropriately, e.g. when running `git status`.

### Pushing
It's good practice to use `git push remote-branch local-branch` rather than just `git push`, as the branch in use might change.

### Staging
 * `git reset HEAD filename` to unstage a file.
 * To undo all changes made to file since the last commit, use `git checkout filename`.

### Tools
Gitk is a great tool for visualising branches and commits.


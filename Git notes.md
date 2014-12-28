Git notes
----------
Some notes on how to set up and use git, specifically geared towards github.

# Setup
## Config
```git
git config --global user.name
git config --global user.email example@email.com
```
The first line will check what username is currently set to git. The second line will **set** the git email to example@email.com. The `--global` flag is used to set the user for all git projects owned by the computers user (`--system` will set it for other users using the same computer as well). `--local` will set the user only for the current repository.

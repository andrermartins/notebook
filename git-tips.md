# Git Tips

## How to pull the right way

1. Always try this, if it works, you're done!
```sh
  git pull --rebase first
```

2. If you get a merge conflict, you can undo everything with:
```sh
  git rebase --abort
```
3. Just pull normally using `git pull`, or do an interactive rebase (advanced)

4. Type this into your terminal to set up:
```sh
git config --global alias.pr "pull --rebase"
```
Now you can use `git pr` instead.

## How to use worktree

1. If you need to switch to another branch and don't want to lose your current work, create a worktree.
```sh
git worktree add ..\your-project-feature -b feature
```
2. Now switch to the new folder and open it in your IDE.
```sh
cd ..\your-project-feature
code .
```
3. Type `git branch` you will see the new branch `feature`, now start working on your new feature.
4. Your previous branch is saved in the original folder of your project, so you don’t need to worry about it.
5. To list worktree, type `git worktree list`. 
6. To remove a worktree, type `git worktree remove ../your-project-feature`.


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

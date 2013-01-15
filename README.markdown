Ever had to stop working in the middle of a feature? Who hasn't? You don't want to push that shit to master. How about creating a quick WIP (work in progress) branch to hold that commit? We can do it in just a few commands:

```bash
git add -A .
git commit -m "WIP"
git push remote +head:WIP
git reset head^
```

Let's walk through this:

1. Stage all files for commit
2. Commit with the message "WIP"
3. Push the head of your current remote to the branch called WIP (the `+` forces the push if WIP isn't inline)
4. Reset back to the previous commit, but leave all changes in place in the working directory

Need to continue working on another machine?

```bash
git fetch
git cherry-pick origin/WIP
git reset head^
```

1. Download the contents of the remote repo without applying it to your local branches
2. Get the last commit from origin/WIP (the one you pushed earlier)
3. Reset back to the last commit leaving all changes in place

That's pretty simple, but wouldn't it be nice to have one command for each task?

## NOW YOU CAN!!

`git-save` gives you two commands to automate the above. When you want to save your work to a wip branch just run:

```
git save
```

git will push your changes to the branch and keep your working directory like you never committed. When you're ready to pick up on another machine, just run:

```
git load
```

and git will pull your latest save and apply to the working directory without any superfluous commits. It's beautiful.

## Configuration

By default, `git-save` will save to/load from `origin/wip`. You can change this by running:

```
git config save.remote origin
git config save.branch <NOT WIP>
```

You can add the `--global` flag if you want to set the remote or branch for all of your repos.

### Contributions

Contributions are welcome. Please be kind and branch before you pull request.

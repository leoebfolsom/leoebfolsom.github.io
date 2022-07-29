## quick note on vim

### How to deal with the editor / file viewer while using command line

Because even if you never use vim voluntarily, it may pop up while you’re using git and the command line.

**If vim pops up when you’re viewing a commit message:** You can use the default commit message by typing `:w` and then `:q`.

**If vim pops up when you’re viewing logs:** You can get back to the command line by typing `q` (no colon).

Now, on to git.

## on to git

### Reorder last two commits

https://stackoverflow.com/questions/33388210/how-to-reorder-last-two-commits-in-git 

```
git rebase -i HEAD~2
```

Next, change the order of the commits in the prompt.

```
pick f4648aee My first commit
pick 00adf09a My second commit
```

to

```
pick 00adf09a My second commit
pick f4648aee My first commit
```

### Push all but the most recent commit

```
git push origin HEAD^:name-of-branch
```

### Push all but the most recent commit AND simultaneously create a new remote branch (and a new PR)

```
git push origin HEAD^:name-of-branch
```

### Add a specific commit to a branch

Replace `<commit-hash>` with a commit hash that you obtain by viewing the git log where that commit can be found.

```
git cherry-pick <commit-hash>
```

### Identify files that differ between two branches
While on a branch, comparing to a branch named `main`:

```
git diff --name-status main
```

### Identify merge conflicts (list of files)

```
git diff --name-only --diff-filter=U
```

### Undoing your last commit
I like to do this in two steps so I can see what’s happening and change my mind at the last minute if needed.


Move the changes from your last commit from "committed" to "unstaged." This moves the head of your current branch back one commit:

```
git reset HEAD~1
```


Then, discard changes in your working directory that are not staged:

```
git checkout -- .
```

### Create a local version of a remote branch

https://stackoverflow.com/a/9537923/5037635 

```
git switch <name-of-remote-branch>
```
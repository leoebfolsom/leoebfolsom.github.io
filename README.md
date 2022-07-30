# command line tools n tips by leo

Hello! I'll add command line tips (not only git) to this page as I come up with them. 
I hope it will be a useful resource for anyone trying to make stuff work while using 
the command line.

If you want to reach out with ideas, suggestions, or whatever else, please do! There are links on [my personal website](https://leoebfolsom.com/) that you can use to reach me.

### command line tools covered in this guide
* [vim](#vim)
* [git](#git)

I'll be updating this frequently as I learn. Tools that are missing or incompletely covered 
will be added/updated over time.

## vim

### How to deal with the vim editor / file viewer while using command line
Because even if you never use vim voluntarily, it may pop up while you’re using git and the command line.

**If vim pops up when you’re viewing a commit message:** You can use the default commit message by typing `:w` and then `:q`.

**If vim pops up when you’re viewing logs:** You can get back to the command line by typing `q` (no colon).

Now, on to git.

## git

### Reorder last two commits
[How to reorder last two commits in git?](https://stackoverflow.com/questions/33388210/how-to-reorder-last-two-commits-in-git)

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

### Push all but the most recent commit and create remote branch with those commits 

```
git push origin HEAD^:name-of-branch
```

### Add a specific commit to a branch

Replace `<commit-hash>` with a commit hash that you obtain 
by viewing the git log where that commit can be found.

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
*I like to do this in two steps so I can see what’s 
happening and change my mind at the last minute if needed.*

Move the changes from your last commit from "committed" to "unstaged." 
This moves the head of your current branch back one commit:

```
git reset HEAD~1
```

Then, discard changes in your working directory that are not staged:

```
git checkout -- .
```

### Create a local version of a remote branch
[Using git switch](https://stackoverflow.com/a/9537923/5037635)

```
git switch <name-of-remote-branch>
```

# command line tools n tips by leo

Hello! I'll add command line tips (not only git) to this page as I come up with them. 
I hope it will be a useful resource for anyone trying to make stuff work while using 
the command line.

If you want to reach out with ideas, suggestions, or whatever else, please do! There 
are links on [my personal website](https://leoebfolsom.com/) that you can use to reach me.

### command line tools covered in this guide
* [vim](#vim)
* [vim while you're using git](#vim-while-youre-using-git)
* [git](#git)
* [chmod](#chmod)

I'll be updating this frequently as I learn. Tools that are missing or incompletely covered will be added/updated over time.

## vim

### editor modes
When using vim, you can either be in one of several modes. Here'll, I'll explain
"insert" and "normal" modes. (I'll add others as I learn about them.)

**Insert mode** is similar to the way you’d normally interact with a text editor.

**Normal mode** means that you can use a variety of commands to navigate the file INCLUDING some commands that actually change the content of the file.

To enter insert mode while viewing a file using vim: type `i` (which stands for "insert").

To exit insert mode and re-enter normal mode: type `esc` (the actual escape button).

### keystrokes

Now, on to some important `vi` keystrokes:

`:w`: Save.

`:q`: Quit.

`:x`: Save and quit.

`D`: Delete an entire line while in view mode.
* [How to Delete a Line in VIM {All, Multiple, Range)](https://phoenixnap.com/kb/how-to-delete-line-vim)

`A`: Move to the end of line and enter “insert” mode (A stands for Append).

If you want to set your command line to use vi keystrokes (which could drive you
nuts, could make your life easier, or could be a way of forcing yourself to
learn those keystrokes), you can do so with this command: set -o vi to activate
it (and set -o emacs to revert).

### Additional reading
* [vim cheat sheet](http://www.viemu.com/vi-vim-cheat-sheet.gif)
* [Vim Editor Modes Explained](https://www.freecodecamp.org/news/vim-editor-modes-explained/)

## vim while you're using git

### How to deal with the vim editor / file viewer while using command line
Because even if you never use vim voluntarily, it may pop up while you’re 
using git and the command line.

**If vim pops up when you’re viewing a commit message:** You can use the default 
commit message by typing `:w` and then `:q`.

**If vim pops up when you’re viewing logs:** You can get back to the command 
line by typing `q` (no colon).

**If you’re viewing a commit message:** You can use the default commit message by typing `:x` which means "save and quit."

**If you’re viewing logs:** You can get back to the command line by typing `q` (no colon).

Now, on to git.

## git

### View all commits on your branch
With all the details:
```
git log
```

Without all that noise:
```
git log --oneline
```



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

### List changes that are staged, but not committed.
This can be useful if you don't remember what you've done, and
you want to write a good commit message on the first go. "staged
but not committed" means you've already executed `git add` but 
not `git commit`.
```
git diff --staged
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

### Generally, how to contribute to an open source package/repo
_Note: each repo will have their own contributing guidelines, and you should 
read the README and/or CONTRIBUTING page in their github repo._

1. Go to the repo you want to contribute to.
2. Create a fork of that repo.
3. Clone the fork to your local machine.
    * The way I organize this is:
        - A main folder called `git` that includes all my git repos.
        - A folder within that `git` folder called `forked_repos` which contains 
        any repos that I have forked.
4. Set the main repo (not your fork) as the upstream remote to your fork, 
following these instructions. This enables you to pull changes from the main repo to your fork.
Most likely, you will want to do this from the main branch of your local repo.
```
git checkout main
git remote add upstream <https://github.com/some-org/some-repo.git>
git fetch upstream
```
You can then merge those changes that you pulled from upstream into whatever you're working
on locally:
```
git pull
git checkout your-wip-branch
git merge main
```
5. Make a change in your fork, and then push to GitHub. GitHub will then allow you to
 open a PR to merge your changes into the main repo.

See [this helpful tutorial](https://www.atlassian.com/git/tutorials/git-forks-and-upstreams) 
for more details on git forks and upstreams. 

### Additional reading
* [Stack Overflow: A good answer about reordering commits](https://stackoverflow.com/a/2740812)
* [Stack Overflow: Undoing recent local commits](https://stackoverflow.com/questions/927358/how-do-i-undo-the-most-recent-local-commits-in-git)
* [Cherry-picking commits](https://www.devroom.io/2010/06/10/cherry-picking-specific-commits-from-another-branch/)
* [Rewriting history using git](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History) (amending commits and messages; reordering commits)

## chmod
Tool for changing the access permissions and the special mode flags of file system objects.

List a file’s permissions:
```
ls -l /path/to/file.sh
```

Give everyone who has access to a file execution permissions:
```
chmod a+x /path/to/file.sh
```

* `a` means "all" users, groups, and other. `a` could be substituted for `ugo` (user, group, others).
* `x` means "execute" permissions (permission to run a file).

Give all users who have access execution permissions. (This is sufficient to allow `root` to execute a file.)
```
chmod u+x /path/to/file.sh
```

### Additional reading
* [How to change directory permissions in Linux ](https://vendr.atlassian.net/wiki/spaces/DATA/pages/2249031686/chmod+permission+management)
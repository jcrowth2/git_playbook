# Welcome to the Git Playbook Repo!

#### As part of your development, this Repo will provide some tutorials and examples for you to get comfortable with Git.

Follow the steps below when instructed to as part of the QR playbook.

### Contents
[Commits / Staging](#commits-/-staging)<br>
[Undoing](#undoing)<br>
[Branching](#branching)<br>
[Interctive Git](#interactive-git)<br>
[Git Blame](#git-blame)<br>


## Commits / Staging
### Exercise: Commits (10 minutes)

Follow the below steps:
1. Create a new branch using the command `git branch my_first_branch` in Git Bash
2. Checkout this branch using `git checkout my_first_branch`
3. Add a text file to this repo called `hello_world.txt`
4. Check the `git status` in Git Bash. Is the result expected?
5. Stage your changes to the repository by using `git add hello_world.txt`
6. Commit your changes using the command `git commit -m "feat: add hello world"`
7. See if your changes are successful by using the command `git log` 
   (press `q` to return to enter commands)
8. Try another commit on the same branch, this time by adding text to the file itself.
9. See your changes in Git Bash by using `git diff`
10. Stage the file using `git add hello_world.txt`
11. Commit your changes using the command `git commit -m "feat: update hello world text"`

(Commit messages are important and allow anyone to understand and follow all changes 
within a repo. There will be more on commit messaging standard practice later.)


Depending on your IDE, there will be a different built-in UI to handle common Git 
commands, such as the above. It may be more convenient to commit changes using this in 
some cases.

See your IDE's own docs for guides on how to run git commands straight from your IDE.

#### Outcome: 

You have successfully cloned a repo, created a branch locally (where all changes 
do not affect the main code base or **master** **branch**) and have made changes and
committed these changes. 

To continue on the git playbook: read and understand the [next chapter in Git Book](
https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository)

Specifically pay attention to:
- Untracked (git is not paying attention to this file until you tell it to)
- Unmodified (git is tracking the file but there are no changes)
- Modified (git is tracking the file and has noticed is has changed - you can use
  `git diff` to see the changes in isolation)
- Staged (the changes that have been made are finalised and are ready to be committed)

Feel free to play around and make some more commits on your branch. This is a local
branch unique to you and your machine, so don't worry about going wrong (on version
control, it's quite hard to do!).

### Questions:
1. How do you move from a modified file to a staged file?
2. How do you move from an untracked file to a staged file?
3. What is the difference between `git status` and `git diff`
4. What is an SHA-1 checksum?
5. What command could I use to commit a modified file in one line?

## Undoing!
### Exercise: Undo / Amend (10 minutes)

The last commit we made should have been adding text to our `hello_world.txt` file.<br>
Suppose we want to update the text because we missed something out that should have
been included the first time around?

1. Make some changes to `hello_world.txt`
2. Stage the changes (see previous section if you need a refresher)
3. Commit the changes as part of the previous commit using `git commit --amend` 
   (this may bring up the text editor for you to rewrite the commit message, if you close
   the text editor it will commit using the previous commit message, if you wish to change it, 
   then edit it directly and save and close it.)
4. Use an appropriate `git log` command in Bash to check you have one updated commit
and the `diff` is as expected. 

What if you have made some changes and want to go back and start fresh?

5. In `hello_world.txt` type "I don't belong here" at the end of the file.
6. Stage the changes
7. Check `git status`
8. Realise you don't want these changes to be staged and remove using the command
`git restore --staged hello_world.txt`
9. Check it worked using `git status`
10. Restore it to the state at the previous commit by using 
   `git restore hello_world.txt`
11. Check it worked using `git status`
   
Note: `git reset` and `git checkout` here can also be used in step 7 and 9 respectively.
Check the docs for how these commands work.

Note: Using `git status` often will be useful, and can give advice on how to undo also!

## Branching
### Exercise: Adding to a Branch:

It is important before any `git checkout` that you have resolved any updates to your files,
otherwise there is a chance they can be lost. `git status` is your friend here. 
Git should warn you if you have modified files that have not been taken care of. But 
these warnings can be neglected with `force`.

1. Checkout the `add_branch_exercise` branch
2. Create a new branch called `add_<name>_to_branch_list` and check it out
3. Add your name to the list in `branching.txt`
4. Stage and Commit your changes with an appropriate commit message. 
5. Merge `add_<name>_to_branch_list` with `add_branch_exercise` (remember you need to
    checkout the branch you wish to be merged into unless both are specified)
6. View your merges in git log using `--graph` 

Another branch exists called `add_logo`. This doesn't contain the `branching` file but 
does contain `SP_logo.png`

7. Merge `add_logo` into `add_branch_exercise`
8. Understand what is different about this merge. Use git log and docs to investigate.
   Of the two, which one is the "fast-forward" and what does it mean?
9. Merge `add_branch_exercise` into `master`.
10. Whilst in the `master` branch or otherwise use `git push` to update the remote with 
your changes!
   
### Exercise: Merge Conflicts:

Two colleagues have been working independently and have been tasked with adding the full
text of "Macbeth" and "Hamlet" to the repo.

There are two branches `macbeth` and `hamlet`

1. Checkout one of these branches.
2. Merge the other branch into it.
3. Follow the advice in Git Book 3.2 and Bash to resolve conflicts!
   (look in the conflicting files for text like:<br>
    <<<<<<< HEAD:<br>
    foo<br>
    =======<br>
    bar<br>
    \>>>>>>>>
4. When you are happy, merge to master and push your changes to the remote. 

Note: For more complex merges with many conflicts it can be easier to use 
`git --mergetool` and configure a useful editor. Or indeed using an IDE. 

If you know for sure beforehand you can merge branches and specify which branch
to overrule conflicts using `ours` or `theirs` as detailed in [the docs](
https://git-scm.com/docs/merge-strategies). But this is generally considered risky. 
You could be dealing with conflicts where the correct resolution is only known by
previous authors, and you should seek support unless you know for certain. 

It is good practice to delete branches when you have merged them. As once merged
both the `master` branch and the new branch are pointing to the same place.
The command for this is: `git branch -d <branch name>`. This will keep your git
history tidy.

### Questions

Using [Git Book](https://git-scm.com/book/en/v2/Git-Branching-Branch-Management) 
and previous docs as a guide.

1. What are blobs and trees and which points to which? 
2. Is a branch a pointer? 
3. Is HEAD a pointer?
4. Can you both be on a branch and on HEAD at the same time? 
5. If you switch branches, doe the branch change or does HEAD change? 
6. What command do I use to show all active branches and how do I know which I am currently
on?
7. How can I see branches that are already merged into my current branch?
Is it okay to delete these branches?
8. How can I force delete a branch I know I definitely don't need?
9. What does `git push --set-upstream` do?
10. What command do I use to rename branches?

## Interactive Git
### Interactive Rebase Exercise: 

A _genius_ has been working on a song in this very repo!<br>
Use `git checkout interactive` to take a look at `lyrics.txt`

Before anyone uses `git push` to upload this song to the `remote repo` for the world to see,
let's try and clean up the artist's commit history.

Task: Using `git rebase -i` and the git book (or other documentation),
clean up the commits in lyrics.txt.

Hints:
1. Keep your commits atomic (i.e. verses and chorus separate)
2. The commit messages could be improved, check it follows advice in the style guide and
   edit them. 
3. Any errors first time round do not need to be addressed in separate commits, make it
seem like the _composition_ was flawless first time around
4. The rebase can be done in one go, but it's perfectly sensible to have a few goes
at rebasing. At any point in the rebase use `git rebase --abort` to have another go.
   
When completed send a screenshot of your git log to a member of Special Projects
to be congratulated (and for any improvements)


###Q: What would happen if you were to try to use `git push` on this branch?<br>
A `git push` alone would FAIL. A normal push to a remote repo will work ONLY if 
you have all the commits in the remote also in local. As we have rewrote history by 
using a rebase, we now have commits in the remote which are not on our machine. You can
test this out by trying `git push` in bash. 

#####Force Push:
We address this issue using *force push* or `git push -f`. This *forces* the remote to
align identically with local, overwriting all history. This command should only be used
if the following are true:

1. There is no-one else currently working off and adding commits this branch.
2. You are completely happy that your rebase is successful.

In this case we should be okay to force push. Try it out in bash!
If you are not sure why **(1.)** is an issue. Then go back to the example in the git book
on [_The Perils of Rebasing_](https://git-scm.com/book/en/v2/Git-Branching-Rebasing).

Instead of merging to master in Bash, force push your `interactive_staging` branch to the 
remote and then create a "PULL REQUEST" in GitHub to merge into master. Check out some
simple GitHub tutorials if you're not sure. 

### Interactive Staging Exercise: 

A colleague has done a big chunk of work and had to move on to another branch and has
stored all his stages in a big `wip` commit. 

Now it's your job to commit them all appropriately and atomically. 

1. Checkout the branch `interactive_staging`
2. Use an appropriate `git reset` to keep all changes that the `wip` commit has created 
   and have them **unstaged**. Make sure you know what `soft`,`hard` and `mixed` do.
   (check out [reset](https://git-scm.com/docs/git-reset))
3. Using `git add -i` and the `p` command. Try to commit everything in order. You will
need to make three separate commits.
   
You know the drill, merge to master and push! (or try out another PR)


### Git Reflog/Reset Questions

1. What is the default `git reset` option (HARD/MIXED/SOFT?)
2. If you use a `HARD` reset on uncommitted changes, do you lose them?
3. What about committed changes?
4. What are the differences between `reset` and `checkout`?
5. If someone has recently accidentally erroneously force pushed onto the remote and 
   removed a lot of the commits you were working on, how could you revert that back?

## Git Blame:
### Git Blame/Log Exercise:

1. Using blame, check to see which commits and when lines 1346 - 1350 of `RJ.txt` were 
last changed.
2. Using an appropriate git log command, find out which commits the string
   "wherefore are thou Romeo?" were introduced in. 
   


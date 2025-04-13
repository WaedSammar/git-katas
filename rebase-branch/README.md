# Git Kata: rebase branch

## Setup

1. Run `source setup.sh` (or `.\setup.ps1` in PowerShell)

## The task

You again live in your own branch, this time we will be doing a bit of juggling with branches, to show how lightweight branches are in git.

1. Which branches exist?
2. Look at the log for the master branch
3. Switch to the uppercase branch
4. How does the log compare to the log on the master branch?
5. Rebase your uppercase branch with the master (`git rebase master`)
6. What did just happen? Draw it!
7. Now switch to the master branch
8. Merge uppercase into master
9. What does the log look like now?

## Solutions

1- 
- *master
-  uppercase

2- 

`git log --oneline --graph --all`

```
* b0e442f (HEAD -> master) Add readme
| * 1273ceb (uppercase) Change greeting to uppercase
|/
* ab029cf Add content to greeting.txt
* 707c3d2 Add file greeting.txt
```

3-

`git checkout uppercase`

**Switched to branch 'uppercase'**

4- 

`git log --oneline --graph --all`
```
* b0e442f (master) Add readme
| * 1273ceb (HEAD -> uppercase) Change greeting to uppercase
|/
* ab029cf Add content to greeting.txt
* 707c3d2 Add file greeting.txt
```

5-

`git rebase master`

**Successfully rebased and updated refs/heads/uppercase**

6- 

After rebase, Git rewrites the history of `uppercase` so that its commits are placed on top of `master`.

7-

`git checkout master`

**Switched to branch 'master'**

8-

`git merge uppercase`
```
Updating b0e442f..84281a0
Fast-forward
 greeting.txt | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
```

9-

`git log --oneline --graph --all`
```
* 84281a0 (HEAD -> master, uppercase) Change greeting to uppercase
* b0e442f Add readme
* ab029cf Add content to greeting.txt
* 707c3d2 Add file greeting.txt
```


## Useful commands

- `git switch <branch-name>`
- `git rebase <branch-name>`
- `git log --oneline --graph --all`
- `git merge <branch-name>`

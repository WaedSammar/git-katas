# Git katas: Git reset
We can manipulate the History very much so. We should only ever tinker with our local history. As publicly release commits must expect to be immutable.

We use reset to unstage change, but we can also do many more different things.

## Setup

1. Run `source setup.sh` (or `.\setup.ps1` in PowerShell)

## Task

1. How does your working directory look like?
2. What does your log look like? What does your stage look like?
3. Try to run `git reset --soft HEAD~1`
4. What happens to your working directory, your log and your stage?
5. Run `git reset --mixed HEAD~1`
6. What happens to your working directory, your log and your stage?
7. Run `git reset --hard HEAD~1`
8. What happens to your working directory, your log and your stage?
9. Now try to use `git revert HEAD~1`
10. What happens to your working directory, your log and your stage?

## Solutions

1- 

`ls`
```
1.txt  10.txt  2.txt  3.txt  4.txt  5.txt  6.txt  7.txt  8.txt  9.txt

```

2- 

`$ git status`
```
On branch master
nothing to commit, working tree clean
```

`$ git log --oneline`
```
7d2a8e9 (HEAD -> master) 10
38fee4a 9
5b90551 8
06f3512 7
51bf1c5 6
d663f4d 5
33e1be7 4
7b464a0 3
04d71a1 2
1c86dd6 1
```

3-

` git reset --soft HEAD~1`

4- 

`git log --oneline`
```
38fee4a (HEAD -> master) 9
5b90551 8
06f3512 7
51bf1c5 6
d663f4d 5
33e1be7 4
7b464a0 3
04d71a1 2
1c86dd6 1
```

`$ git status`
```
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   10.txt


```
### 🧠 What happened?

🔁 The last commit ("10") was removed from the log.

📂 The file 10.txt is now in the staging area (ready to be committed again).

✅ Working directory is unchanged


5-


`$ git reset --mixed HEAD~1`

```
$ git log --oneline
5b90551 (HEAD -> master) 8
06f3512 7
51bf1c5 6
d663f4d 5
33e1be7 4
7b464a0 3
04d71a1 2
1c86dd6 1
```
**The last commit (9) was removed from the log.**

6-

`$ git status`
```
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        10.txt
        9.txt

nothing added to commit but untracked files present (use "git add" to track)

```

### 🧠 What happened here?
🔸 Files 9.txt and 10.txt are now untracked.

🔸 This means they were removed from the staging area but still exist in the working directory.


7-

`$ git reset --hard HEAD~1`

**HEAD is now at 06f3512 7**

### 🧠 What happened here?
🔸 Git forcefully moved the HEAD to the previous commit (7)

🔸 This erased the commit 8 and removed its changes from both staging and working directory.

8-

```
$ git log --oneline
06f3512 (HEAD -> master) 7
51bf1c5 6
d663f4d 5
33e1be7 4
7b464a0 3
04d71a1 2
1c86dd6 1
```
**🔸 The log shows that commit 8 is now gone.**

`$ git status`
```
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        10.txt
        9.txt

nothing added to commit but untracked files present (use "git add" to track)
```

### 🧠 Working Directory:
🔸 Even though we ran --hard, files 9.txt and 10.txt are still here but as untracked.

🔸 Why? Because they were already untracked before the --hard, so Git doesn't manage them.


9-

`$ git revert HEAD~1`
```
[master cfe15e4] Revert "6"
 1 file changed, 1 deletion(-)
 delete mode 100644 6.txt
```
🔸 Git created a new commit with the message Revert "6"

🔸 This commit undid the changes made in commit 6, which means it deleted the file 6.txt.

10-

`$ git log --oneline`

```
cfe15e4 (HEAD -> master) Revert "6"
06f3512 7
51bf1c5 6
d663f4d 5
33e1be7 4
7b464a0 3
04d71a1 2
1c86dd6 1
```

### 🧠 Log explanation:

- Commit 6 is still part of the history—it was not removed.

- Instead, a new commit was added to reverse its changes.

- This makes git revert a safe operation for public/shared history (e.g., on GitHub).

`$ git status`
```
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        10.txt
        9.txt

nothing added to commit but untracked files present (use "git add" to track)
```

`$ ls`
```
1.txt  10.txt  2.txt  3.txt  4.txt  5.txt  7.txt  9.txt

```

### 📌 Notice:

- 6.txt is gone (because the commit that added it was reverted).

- Files 9.txt and 10.txt are still present as untracked files.


## Useful commands

- `git log --oneline`
- `git commit --amend`
- `git status`
- `git reset --soft`
- `git reset --mixed`
- `git reset --hard`
- `git revert`

## Further explanation

The following is taken from Recap section of [https://git-scm.com/book/en/v2/Git-Tools-Reset-Demystified].
The reset command overwrites these three trees in a specific order, stopping when you tell it to:
1. Move what the branch HEAD points to (stop here if --soft)
2. Make the stage look like HEAD (stop here unless --hard)
3. Make the working directory look like the stage

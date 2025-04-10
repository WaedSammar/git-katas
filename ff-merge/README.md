# Git Kata: Fast-forward Merge

## Setup

1. Run `source setup.sh` (or `.\setup.ps1` in PowerShell)

## The task

You again live in your own branch, this time we will be doing a bit of juggling with branches, to show how lightweight branches are in git.

1. Create a (feature)branch called `feature/uppercase` (yes, `feature/uppercase` is a perfectly legal branch name, and a common convention).
2. Switch to this branch
3. What is the output of `git status`?
4. Edit the greeting.txt to contain an uppercase greeting
5. Add `greeting.txt` files to staging area and commit
6. What is the output of `git branch`?
7. What is the output of `git log --oneline --graph --all`

   *Remember: You want to update the master branch so it also has all the changes currently on the feature branch. The command 'git merge [branch name]' takes one branch as argument from which it takes changes. The branch pointed to by HEAD (currently checked out branch) is then updated to also include these changes.*

8. Switch to the `master` branch
9. Use `cat` to see the contents of the greetings
10. Diff the branches
11. Merge the branches
12. Use `cat` to see the contents of the greetings
13. Delete the uppercase branch

### Solutions:

1- `git branch feature/uppercase`

2- `git checkout feature/uppercase`

3- 
```
On branch feature/uppercase
nothing to commit, working tree clean
```
4- ` notepad greeting.txt`

**write inside it HELLO, WELCOME TO THE GIT KATA!**

5- 
```
git add greeting.txt
git commit -m "Update file with uppercase"
```
6- 
```
feature/uppercase 
master //The output confirms that the currently active branch is feature/uppercase.
```
7-
```
* aac78d1 (HEAD -> feature/uppercase) Update file with uppercase
  - This commit is on the `feature/uppercase` branch, where you updated the `greeting.txt` file to contain an uppercase greeting message.

* 4034fb9 (master) Add content to greeting.txt
  - This commit is on the `master` branch, where content was added to the `greeting.txt` file.

* 1f35fe1 Add file greeting.txt
  - This is the initial commit where the `greeting.txt` file was first created and added to the repository.

```

8- `git checkout master`

9-
``` 
cat greeting.txt 
hello
```
10- 

`git diff feature/uppercase`
```
diff --git a/greeting.txt b/greeting.txt
index 0b14818..ce01362 100644
--- a/greeting.txt
+++ b/greeting.txt
@@ -1,2 +1 @@
 hello
-HELLO, WELCOME TO THE GIT KATA :)
```
11-

`git merge feature/uppercase`
```
Updating 4034fb9..aac78d1
Fast-forward
 greeting.txt | 1 +
 1 file changed, 1 insertion(+)
```
12-

`cat greeting.txt`
```
hello
HELLO, WELCOME TO THE GIT KATA :)
```

13-

`git branch -d feature/uppercase`

`Deleted branch feature/uppercase (was aac78d1).`


## Useful commands

- `git branch`
- `git branch <branch-name>`
- `git branch -d <branch-name>`
- `git switch`
- `git branch -v`
- `git add`
- `git commit`
- `git commit -m`
- `git merge <branch>`
- `git diff <branchA> <branchB>`
- `git log --oneline --graph --all`

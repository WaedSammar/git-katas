# Git Kata: Basic revert
## Setup:

1. Run `source setup.sh` (or `.\setup.ps1` in PowerShell)

## The task

In this task a few changes snuck in, that we'd like to get out. Our history is public, so we can't just change it. Rather we need to use revert to remove the unwanted changes in a safe way.

1. Use `git log --oneline` to look at the history
2.  Use `cat` to view the content of `greeting.txt`
3.  Use `git revert` on the newest commit, to remove the changes the last commit added
4.  Use `git log --oneline` to view the history
5.  Did the revert command add or remove a commit?
6.  Use `cat` to view the content of `greeting.txt`
7.  Use `ls` to see the content of the workspace
8.  Use `git log --oneline` to find the sha of the commit adding credentials to the repository
9.  Use `git revert` to revert the commit that added the credentials
10. Use `git log --oneline` to view the history
11. Use `ls` to see the content of the workspace
12. How many commits were added or changed by the last revert?
13. Use `git show` with the sha of the commit you reverted to see that the credentials file is stilll in the history
14. As you have now reverted the credentials file, so it is removed from your working directory, is it also removed from git?

## Solutions

1- 

`git log --oneline`
```
1182216 (HEAD -> master) Overwrite greeting.txt
79d8d3a Add content to greeting.txt
80f01e1 Add credentials to repository
d94221f Add file greeting.txt
```

2- 

`cat greeting.txt`

**This should have been appended to the original content, rather than overwriting it**

3-

`git revert HEAD`

```
[master 60ad088] Revert "Overwrite greeting.txt"
 1 file changed, 1 insertion(+), 1 deletion(-)
```

4- 

`git log --oneline`
```
60ad088 (HEAD -> master) Revert "Overwrite greeting.txt"
1182216 Overwrite greeting.txt
79d8d3a Add content to greeting.txt
80f01e1 Add credentials to repository
d94221f Add file greeting.txt

```

5-


#### The `git revert` command added a new commit — it did not remove the original one.

It created a new commit that reverses the changes introduced by the previous commit,
but it keeps the original commit in the history to preserve the commit timeline, which is especially important in public/shared repositories.

6- 

`cat greeting.txt`

**Original file content**


7-

`ls`

- **credentials.txt**  
- **greeting.txt**

8-

`git log --oneline`
```
60ad088 (HEAD -> master) Revert "Overwrite greeting.txt"
1182216 Overwrite greeting.txt
79d8d3a Add content to greeting.txt
80f01e1 Add credentials to repository
d94221f Add file greeting.txt

```

9-

```
🔑 SHA: 80f01e1
📄 Message: Add credentials to repository

```

`git revert 80f01e1`
```
[master d2267a0] Revert "Add credentials to repository"
 1 file changed, 1 deletion(-)
 delete mode 100644 credentials.txt
```

10-

`git log --oneline`
```
d2267a0 (HEAD -> master) Revert "Add credentials to repository"
60ad088 Revert "Overwrite greeting.txt"
1182216 Overwrite greeting.txt
79d8d3a Add content to greeting.txt
80f01e1 Add credentials to repository
d94221f Add file greeting.txt
```

11-

`ls`

**greeting.txt**  
//the file credentials.txt deleted

12-

- The last git revert (on commit 80f01e1) added only one commit.

- This commit was created to reverse the changes made by the commit that added the credentials. Therefore, only one commit was added to undo the changes.

13-

`git show 80f01e1`
```
commit 80f01e1d1550eef6367106ff9257134cb13a1528
Author: git-katas trainer bot <git-katas@example.com>
Date:   Sun Apr 13 11:02:13 2025 +0300

    Add credentials to repository

diff --git a/credentials.txt b/credentials.txt
new file mode 100644
index 0000000..8995708
--- /dev/null
+++ b/credentials.txt
@@ -0,0 +1 @@
+supersecretpassword
```

14-

- No, the credentials file is not removed from Git history.

- While the file was removed from the working directory, the commit that added the credentials (80f01e1) still exists in the history. The git revert command only creates a new commit that undoes the changes, but it does not remove the original commit from the repository's history.

So, the file is no longer in working directory, but it remains part of Git's historical record.

## Useful commands
- `git revert <ref>`
- `git log --oneline`
- `git show <ref>`

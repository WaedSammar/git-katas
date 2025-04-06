# Git Kata: Basic Staging

This kata will examine the staging area of git.

In git we are working with three different areas:

* The working directory where you are making your changes
* The staging area where all changes you have added through `git add` will stay
* The repository where every commit ends up, making your history. To put your staged changes in here you issue the `git commit` command.

A file can have changes both in the working directory and staging area at the same time.
These changes do not have to be the same.

We will also work with `git restore` to restore the staged changes of a file, and `git checkout` to return a file to a previous state.

## Setup

1. Run `source setup.sh` (or `.\setup.ps1` in PowerShell)

## The task

You live in your own repository. There is a file called `file.txt`.

1. What's the content of `file.txt`?
```
$ cat file.txt
1
```
2. Overwrite the content in `file.txt`: `echo 2 > file.txt` to change the state of your file in the working directory (or `sc file.txt '2'` in PowerShell)
3. What does `git diff` tell you?
```
diff --git a/file.txt b/file.txt
index 20f1f68..0cfbf08 100644
--- a/file.txt
+++ b/file.txt
@@ -1 +1 @@
-1
+2
```
4. What does `git diff --staged` tell you? why is this blank?

Because `git diff --staged` shows the difference between the staged changes and the last commit and I haven't run `git add file.txt` yet
5. Run `git add file.txt` to stage your changes from the working directory.
6. What does `git diff` tell you?
No Output 

7. What does `git diff --staged` tell you?
The difference between the staged version of file.txt and the last commit

8. Overwrite the content in `file.txt`: `echo 3 > file.txt` to change the state of your file in the working directory (or `sc file.txt '3'` in PowerShell).
9. What does `git diff` tell you?
Show that file.txt has been changed from 2 to 3

10. What does `git diff --staged` tell you?
No Output
11. Explain what is happening
#### `git diff` → The difference between currently modified files and those ready to be added (staged).
#### `git diff` --staged → The difference between staged files and the last commit.

12. Run `git status` and observe that `file.txt` are present twice in the output.
13. Run `git restore --staged file.txt` to unstage the change
14. What does `git status` tell you now?
15. Stage the change and make a commit
16. What does the log look like?
```
Waed@Waed MINGW64 ~/basic-staging/git-katas/basic-staging/exercise (master)
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   file.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   file.txt

commit 9006a356771abe920cb0d467d4577370a6d01f6f (HEAD -> master)
Author: Waed Sammar <waedsammar12@gmail.com>
Date:   Sun Apr 6 13:05:31 2025 +0200

    update file to 3

commit b8961e68b5e94537573cdcc8ed89ea3bb5afd8e2
Author: Waed Sammar <waedsammar12@gmail.com>
Date:   Sun Apr 6 12:40:12 2025 +0200

    update file

commit cd81b9e1446f875780a4742cbb724d54aaeca8c3
Author: Waed Sammar <waedsammar12@gmail.com>
Date:   Sun Apr 6 12:36:46 2025 +0200

    initial commit

commit b8ce437d87b40418508116b4f3de12cb8821a77a
Author: git-katas trainer bot <git-katas@example.com>
Date:   Sun Apr 6 12:24:03 2025 +0200

    1
:...skipping...
commit 9006a356771abe920cb0d467d4577370a6d01f6f (HEAD -> master)
Author: Waed Sammar <waedsammar12@gmail.com>
Date:   Sun Apr 6 13:05:31 2025 +0200

    update file to 3

commit b8961e68b5e94537573cdcc8ed89ea3bb5afd8e2
Author: Waed Sammar <waedsammar12@gmail.com>
Date:   Sun Apr 6 12:40:12 2025 +0200

    update file

commit cd81b9e1446f875780a4742cbb724d54aaeca8c3
Author: Waed Sammar <waedsammar12@gmail.com>
Date:   Sun Apr 6 12:36:46 2025 +0200

    initial commit

commit b8ce437d87b40418508116b4f3de12cb8821a77a
Author: git-katas trainer bot <git-katas@example.com>
Date:   Sun Apr 6 12:24:03 2025 +0200

    1
~
~
~
commit 9006a356771abe920cb0d467d4577370a6d01f6f (HEAD -> master)
Author: Waed Sammar <waedsammar12@gmail.com>
Date:   Sun Apr 6 13:05:31 2025 +0200

    update file to 3

commit b8961e68b5e94537573cdcc8ed89ea3bb5afd8e2
Author: Waed Sammar <waedsammar12@gmail.com>
Date:   Sun Apr 6 12:40:12 2025 +0200

    update file

commit cd81b9e1446f875780a4742cbb724d54aaeca8c3
Author: Waed Sammar <waedsammar12@gmail.com>
Date:   Sun Apr 6 12:36:46 2025 +0200

    initial commit

commit b8ce437d87b40418508116b4f3de12cb8821a77a
Author: git-katas trainer bot <git-katas@example.com>
Date:   Sun Apr 6 12:24:03 2025 +0200

    1

```
17. Overwrite the content in `file.txt`: `echo 4 > file.txt` (or `sc file.txt '4'` in PowerShell)
18. What is the content of `file.txt`?
4
19. What does `git status` tell us?
The changes not staged for commit

20. Run `git restore file.txt`
21. What is the content of `file.txt`?
3

22. What does `git status` tell us?
```
On branch master
nothing to commit, working tree clean
```
## Useful commands

- `git add`
- `git commit`
- `git commit -m "My lazy short commit message"`
- `git log`
- `git log -n 5`
- `git log --oneline`
- `git log --oneline --graph`
- `git restore --staged`

## Aliases

You can set up aliases as such:
`git config --global alias.lol 'log --oneline --graph --all'`
This might be useful to you.

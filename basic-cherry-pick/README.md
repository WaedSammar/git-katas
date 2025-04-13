# Git Kata: Basic Cherry Pick

In this task we want have two branches, master and feature. We have worked and progressed on both branches seperately. However, there are a few changes on the feature branch that we want to take and add onto the master branch. Without getting the entire changeset from the feature branch.

Git has functionality for this "take-just-these-changes" and it is called `cherry-pick`.
You tell Git which commits you would like to cherry pick and Git will add those commits onto your branch's commit history.

Git can cherry pick either a single commit or a range of commits from a branch.

## Setup:

1. Run `source setup.sh` (or `.\setup.ps1` in PowerShell)

## The task


We currently have this git history in our exercise repository :

    A - B - C - D         master
          \
            E - F - G - H feature

As you can see the `feature` branch and the `master` branch have progressed with different commits. We want to cherry pick the commits F and G and add them onto the master branch, so that our Git history looks like this:

    A - B - C - D - F - G master
          \
            E - F - G - H feature

1. Use `git log --oneline --graph --all` to look at the history
2. Use `cat` to view the content of `names.txt`. This file is changed in commit F
3. Use `cat` to view the content of `sentence.txt`. This file is changed in commit G
4. Use `git cherry-pick <commit_hash_F>` to cherry pick just the F commit onto your branch
5. Use `git log --oneline` to see the change to the history and that commit F should now be the newest commit on the master branch
6. Use `cat` to view the content of `names.txt` look how it has now changed!
7. Use `git reset --hard HEAD^` to delete that cherry picking from the history so that we can now try again and cherry pick a range of commits
8. Use `git log --oneline --graph` to check the the cherry picked commit is now removed from the branch
9. We are now essentially back to where we began, now use `git cherry-pick <commit_hash_F>^..<commit_hash_G>` to cherry pick the range of commits from F to G (the two commits). Pay close attention and do not forget the caret `^` symbol after the first commit hash (see the section *Useful Note* below to understand why this is needed)
10. Use `git log --oneline --graph` to view the history
11. Use `cat` to view the contents of `names.txt` and `sentence.txt` look how they have changed!
12. How many commits were added due to the cherry pick?

## Solution:

1-

`git log --oneline --graph --all`
```
* 3b85b27 (feature) Commit H: Added the boring file
* ce1efbb Commit G: Updated the original sentence file
* 484f7b0 Commit F: Updated and added more names to the file
* d46ee27 Commit E: Added the numbers file
| * 90f9f84 (HEAD -> master) Commit D: Added the animals file
| * c5424fb Commit C: Added the additional other_sentence file
|/
* 05346ae Commit B: Added the sentence file
* 70ebaf1 Commit A: Added the names file
```

2-

`$ cat names.txt`
```
Ben
Tom
Sally
```

3-

`cat sentence.txt`

`This is a lovely sentence`

4-

`git cherry-pick 484f7b0`
```
[master 74fe5fd] Commit F: Updated and added more names to the file
 Author: git-katas trainer bot <git-katas@example.com>
 Date: Sun Apr 13 16:47:46 2025 +0300
 1 file changed, 3 insertions(+)
```

5-

`git log --oneline`
```
74fe5fd (HEAD -> master) Commit F: Updated and added more names to the file
90f9f84 Commit D: Added the animals file
c5424fb Commit C: Added the additional other_sentence file
05346ae Commit B: Added the sentence file
70ebaf1 Commit A: Added the names file
```

6-

`cat names.txt`
```
Ben
Tom
Sally
Craig
Jodie
Nathan
```
7-

`git reset --hard HEAD^`

`HEAD is now at 90f9f84 Commit D: Added the animals file`

8-

`git log --oneline --graph`
```
* 90f9f84 (HEAD -> master) Commit D: Added the animals file
* c5424fb Commit C: Added the additional other_sentence file
* 05346ae Commit B: Added the sentence file
* 70ebaf1 Commit A: Added the names file
```

9-

 `git cherry-pick 484f7b0^..ce1efbb`
 ```
[master f3454d2] Commit F: Updated and added more names to the file
 Author: git-katas trainer bot <git-katas@example.com>
 Date: Sun Apr 13 16:47:46 2025 +0300
 1 file changed, 3 insertions(+)
[master f7eda9c] Commit G: Updated the original sentence file
 Author: git-katas trainer bot <git-katas@example.com>
 Date: Sun Apr 13 16:47:46 2025 +0300
 1 file changed, 1 insertion(+)
```

10-

`git log --oneline --graph`
```
* f7eda9c (HEAD -> master) Commit G: Updated the original sentence file
* f3454d2 Commit F: Updated and added more names to the file
* 90f9f84 Commit D: Added the animals file
* c5424fb Commit C: Added the additional other_sentence file
* 05346ae Commit B: Added the sentence file
* 70ebaf1 Commit A: Added the names file
```

11-

- `cat names.txt`
```
Ben
Tom
Sally
Craig
Jodie
Nathan
```

- `cat sentence.txt`
```
This is a lovely sentence
Finally I think this is probably the last sentence to add
```

12- **Two commits were added to the master branch due to the cherry pick: Commit F and Commit G.**


## Useful Note

When using range of commits with the cherry pick command, the first commit hash specified for the oldest (left side of the range) is not actually included in the cherry pick, as in that commit is excluded but all others between and including the newest commit are.

So to bypass this issue it is useful to use the caret `^` after the first commit hash to tell Git that you want the commit BEFORE this commit, therefore including it in the cherry pick process.

For example

    git cherry-pick ABCD..EFGH

would not include the commit ABCD, instead you should add a caret symbol to the end of the ABCD to tell git to include it, like this:

    git cherry-pick ABCD^..EFGH

Reference: https://www.tollmanz.com/git-cherry-pick-range/
Reference: https://git-scm.com/docs/git-cherry-pick

## Useful commands
- `git cherry-pick <ref>`
- `git reset --hard <ref>`
- `git log --oneline --graph --all`

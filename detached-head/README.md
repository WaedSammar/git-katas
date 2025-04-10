# Detached head state

When a user ends up in a "detached head" state, this is a scary situation, but as we know, Git is not scary.

## Setup:

1. Run `source setup.sh` (or `.\setup.ps1` in PowerShell)

## The task

1. Run `git status` and `git log --oneline --graph --all` to see what is going on.
2. Restore normalcy in this repository by moving to `master`

Note that this task might seem more confusing if you did not run `setup.sh` in your terminal.

We want to have a branch called `the-beginning` that is made from the first commit with message `A`. 

3. Can you do this by first causing a detached head?

### Solutions:

1- 
- `git status`

    ```
    HEAD detached at 2b5221c
    nothing to commit, working tree clean
    ```

- `git log --oneline --graph --all`
    ```
    * ba830e2 (master) D          # Latest commit on the master branch
    * ea8643c C                   # Commit before D, message: C
    * 2c916e2 B                   # Commit before C, message: B
    * 2b5221c (HEAD) A            # First commit in the repo, currently checked out (detached HEAD)
    ```

2- 

`git checkout master`

```
Previous HEAD position was 2b5221c A
Switched to branch 'master'
```

3- 

- `git checkout 2b5221c`

    ```
    Note: switching to '2b5221c'.

    You are in 'detached HEAD' state. You can look around, make experimental
    changes and commit them, and you can discard any commits you make in this
    state without impacting any branches by switching back to a branch.

    If you want to create a new branch to retain commits you create, you may
    do so (now or later) by using -c with the switch command. Example:

    git switch -c <new-branch-name>

    Or undo this operation with:

    git switch -

    Turn off this advice by setting config variable advice.detachedHead to false

    HEAD is now at 2b5221c A

    ```
- `git switch -c the-beginning`

    `Switched to a new branch 'the-beginning'`

- `git merge the-beginning`

    `Already up to date.`
- `git log --oneline --graph --all`
    ```
    * ba830e2 (HEAD -> master) D
    * ea8643c C
    * 2c916e2 B
    * 2b5221c (the-beginning) A
    ```

## Useful commands

- `git status`
- `git log --oneline --graph --all`
- `git checkout <ref>` or `git switch --detach <ref>`

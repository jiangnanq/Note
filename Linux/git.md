---
title: Git Command list
date: 2017-6-8
tags: Git
---

- Local command
  * Reverting Working Copy to Most Recent Commit
    To revert to previous commit, ignoring any changes:
    ```
    git reset --hard HEAD
    ```
    where HEAD is the last commit in your current branch
  * Reverting Working Copy to an Older Commit. To revert to a commit that's older than the most recent commit:
  * Resets index to former commit; replace '56e05fced' with your commit code
    ```
    git reset 56e05fced 
    ```
  * Moves pointer back to previous HEAD
    ```bash
    git reset --soft HEAD@{1}
    git commit -m "Revert to 56e05fced"
    ```
  * Updates working copy to reflect the new commit
    ```bash
    git reset --hard
    ```

  * Switch to previous version
    Revert back to previous version:
    Don't forget the . in the end.
    ```
    git checkout [reversion] .
    ```
    Revert back to master version:
    ```
    git reset --hard;
    ```

    Remove cached file from repo (Not from local file)
    ```
    git rm --cached fileToBeRemoved
    ```

- Remote command
  * SSH key (required for remote access)
    [Check SSH exist](https://help.github.com/articles/checking-for-existing-ssh-keys/)
    [Add SSH key to GITHUB account](
    https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/#adding-your-ssh-key-to-the-ssh-agent)

  * Add remote source
    Setup a new remote
    ```
    git remote add origin https://github.com/user/repo.git
    ```
    Verify new remote
    ```
    $ git remote -v
    $ origin  https://github.com/user/repo.git (fetch)
    $ origin  https://github.com/user/repo.git (push)
    ```
    Push to remote 
    ```
    $ git push origin master
    ```
    Pull from remote
    ```
    $ git pull 
    ```
  * Add existing project to remote
    1. Create repository on the github
    2. Commit existing project
    ```
    git remote add origin urlofgithub
    git push -u origin master
    ```

- Git Branch
  * Create branch and switch to it
    ```
    git checkout -b newbranchname
    ```
  * After add/commit on the branch, need to switch back to master and merge them
    ```
    git checkout master
    git merge newbranchname
    ```
  * Delete branch
    ```
    git branch -d branchname
    ```
  * Merge master to branch
    ```
    git checkout branchname
    git rebase master
    ```

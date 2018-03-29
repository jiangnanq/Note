
# Git command list

## Reverting Working Copy to Most Recent Commit
  1. To revert to previous commit, ignoring any changes:
    ```
      git reset --hard HEAD
    ```
  where HEAD is the last commit in your current branch

## Reverting Working Copy to an Older Commit
  1. To revert to a commit that's older than the most recent commit:
    * Resets index to former commit; replace '56e05fced' with your commit code
      ```
      git reset 56e05fced 
      ```
    * Moves pointer back to previous HEAD
      ```
      git reset --soft HEAD@{1}
      git commit -m "Revert to 56e05fced"
      ```
    * Updates working copy to reflect the new commit
      ```
      git reset --hard
      ```

## Switch to previous version
  1. Revert back to previous version:
      ```
      git checkout [reversion] .
      Don't forget the . in the end.
      ```
  2. Revert back to master version:
      ```
      git reset --hard;
      ```

##  SSH key (required for remote access)
  1. [Check SSH exist](https://help.github.com/articles/checking-for-existing-ssh-keys/)
  2. [Add SSH key to GITHUB account](
  https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/#adding-your-ssh-key-to-the-ssh-agent)

## Push to remote 
  ```
  $ git push origin master
  ```

## Pull from remote
  ```
  $ git pull 
  ```
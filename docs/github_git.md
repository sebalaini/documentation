# GitHub / git

- Create useful [.gitignore](https://www.toptal.com/developers/gitignore) files for your project.
- Reset local changes alias.
  ```bash
  alias nah="git reset HEAD --hard && git checkout . && git clean -df ."
  ```
- Git amend last commit using last message & push alias.
  ```bash
  alias gitamendforce="git add . && git commit --amend --no-edit && git push --force"
  ```
  The `--no-edit` reuse the last commit message.<br>
  If you want to squash multiple commit you need to run this command:
  ```bash
  $ git rebase -i HEAD~3 #where 3 is the number of commit to merge
  ```

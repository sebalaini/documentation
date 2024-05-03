# GitHub / git

## Commands

- Create useful [.gitignore](https://www.toptal.com/developers/gitignore) files for your project.
- Reset local changes (alias).
  ```bash
  alias nah="git reset HEAD --hard && git checkout . && git clean -df ."
  ```
- Git amend last commit using last message & push (alias).
  ```bash
  alias gitamendforce="git add . && git commit --amend --no-edit && git push --force"
  ```
  The `--no-edit` reuse the last commit message.<br>
  If you want to squash multiple commit you need to run this command instead:
  ```bash
  $ git rebase -i HEAD~3 #where 3 is the number of commit to merge
  ```
- Git delete local branches (alias)
  ```bash
  alias gitcleanlocalbranches="git fetch --prune origin && git branch -vv | awk '/: gone]/{print $1}' | xargs git branch -D"
  ```
  This command has to be ran on the main branch, the above command uses the `-D` instead of `-d` because there are cases where the command returns an error saying: The branch `xxx` is not fully merge. If you are sure you want to delete it, run `git branch -D xxx`.

## SSH key auth

- Open Terminal and run the below code:

  ```
  ssh-keygen -t ed25519 -C "your_email@example.com"
  ```

  This creates a new SSH key, using the provided email as a label.

  - When you're prompted to "Enter a file in which to save the key", you can press Enter to accept the default file location.

  - At the prompt, type a secure passphrase. For more information, see "Working with SSH key passphrases." or continue without a passphrase

- You will need to modify your `~/.ssh/config` file to automatically load keys into the ssh-agent and store passphrases in your keychain.

  - add this code to it:
    ```
    Host github.com
      AddKeysToAgent yes
      UseKeychain yes
      IdentityFile ~/.ssh/id_ed25519 # replace with your key's name
    ```

- Go to your profile [SSH & GPG keys](https://github.com/settings/keys) page.
  - Add new SSH key
  - Copy your previously created SSH key, you need to copy the `id_ed25519.pub` one.

More info available in the [GitHub Doc](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

## remove GitHub attachment

You can remove uploaded attachment via the GitHub Virtual Agent.

- [file attachment](https://support.github.com/?q=remove+file+attachment)
- [image attachment](https://support.github.com/?q=remove+image+attachment)

## Badges generator

- [Michael Currin badge generator](https://michaelcurrin.github.io/badge-generator/#/)

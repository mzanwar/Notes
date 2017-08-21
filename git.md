# Git:

`git reset --soft HEAD^` -> put all changes back into `staging git reset --hard HEAD^` -> discard all changes on last commit, move to previous commit

`git commit --amend -m "Some message"` -> amend latest commit

`git pull` -> `git fetch` then `git merge origin/master`

`git remote show origin`

`git branch -r` -> see all remote branches

`git push origin :weasel` -> deletes remote branch

Tagging: git tag git tag -a v1.0 -m "Version 1.0" git push --tags

####Rebase:
Conceptually, you're changing the base of the branch you're on. Everything is changing on the branch we call this from; nothing changes on the branch after the rebase command.

1. Find common commit shared among both branches
2. Put all commits ahead of shared commit in a temp folder (this is done on branch we're working from)
3. Put all commits ahead on shared commit on the other branch on local branch
4. Put all commits from temp onto local branch

If merge conflict, resolve conflict, add file and git rebase --continue

`git log -p `-> show patches

`git aliases`

####Interactive Rebase:
(it applies these rules as it pulls commit off the temp queue from above)
`git rebase -i HEAD~3` -> last three commits

`pick` -> pick and apply

`reword` -> change commit message

`edit` -> replay command but stop before committing (we can split up commits)

`squash` -> squash commit with previous commit

####Stashing:
`git stash save [message]` ->

`git stash`

`git stash apply`

`git stash drop`


`git stash pop` -> apply + pop off stack (this is the one you use)

`git stash --include-untracked`-> all untracked files


`git stash --keep-index` -> only staging files?

`git stash list --stat`

`git stash show [name]` -> any option that the git log command takes (ie. --patch)
`git stash branch branch-name [stash`]
`git stash clear`


####Purging History: Filtering:

Before doing anything -> 1. `git clone repo` backup repo

`git filter-branch --tree-filter <command>` -> checks out each commit, runs your command against it and recommits

`git filter-branch --tree-filter 'rm -f passwords.txt' -- --all` (runs against all commits in all branches)
If the command fails for any reason; the whole filter will fail (so we added a -f to out rm to mitigate this)

`git filter-branch --index-filter <command>` -> only puts stuff in staging; so need commands that run against staging: 'git rm --cached --ignore-unmatched passwords.txt'

`git filter-branch --index-filter 'git rm --cached --ignore-unmatch master_password.txt' -- --all`

`git filter-branch -f --index-filter` -> if it can't overwrite

`git filter-branch -f --prune-empty -- --all` -> remove all empty commits

####.gitattributes File

text conversion windows to unix

`git config --global core.autocrlf input`

`git config --global core.autocrlf true`

####Cherry Picking

1. Checkout branch you want to apply the commit to

`git cherry-pick --no-commit -x --signoff [shas; can be multiple]`

`--edit`         -> change commit message

`--no-commit` -> put changes into staging and manually commit

`-x  `           -> leave sha in there

`---signoff `    -> make sure the user who did the cherrypicking is also in there

####Reflog:
`git reflog` -> never deletes a commit
`git reset --hard <shaname>`

`git log --walk-reflogs`

`git branch name sha</shaname>`

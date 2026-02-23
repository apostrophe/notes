**Terminology**
head_ref - source branch name?
base_ref - destination branch name?

cool_new_feature -> dev
head_ref -> base_ref

example of it used here:
/Users/benjamin.schilke/repos/pricing-operations/pricera-backend/.github/workflows/determine-changes.yml

```bash
git config --list
git config --get credential.helper
git config set user.name "Ben Schilke2"


# display ssh auth verbose mode
git config --get core.sshCommand 
# enable verbose mode with ssh auth
git config core.sshCommand "ssh -v" # -v, -vv, -vvv
# disable
git config --unset core.sshCommand
# or include in GIT_SSH_COMMAND (use -vvv for extreme verbose)
GIT_SSH_COMMAND='ssh -v -i ~/.ssh/keypair' git push origin master

# specify specific key-pair
GIT_SSH_COMMAND='ssh -i ~/.ssh/keypair' git push origin master
```

**2 accounts on Mac - Solution** -> See Simpler Approach (below)
1. Deactivate ~/.ssh/config file (renamed to con_fig)
2. add to ssh-agent:
    `ssh-add --apple-use-keychain ~/.ssh/worklaptop-apostrophe-github-acct`
    view current list:
      `ssh-add -l`
3. run command with key explictly mentioned:
    `GIT_SSH_COMMAND='ssh -i ~/.ssh/worklaptop-apostrophe-github-acct' git push -u origin main`

**Simpler Approach**
1. Give 'ikea' user account access to personal repo
2. Commit using this account


**Standard Commands**
```bash
git push origin feature/CWEL-565-update-order-status
```

**Branches**
```bash
git branch # list all local branches
git branch -r # list remote branches
git branch -a # list all branches (local and remote)
git branch -v # list remote branches verbose

```


**Remove Repos and Branches**

```bash

local repo       url            remote repo
                 ----->         git@github.com:ingka-group-digital/pricera-frontend.git
--------------                  --------------
| main       |    branch        | main       |
|            |    --->          |            |
--------------                  --------------


# list the remote branches - origin is automatically added when cloning a repo
$ git remote
origin

$ git remote --verbose
origin  git@github.com:ingka-group-digital/pricera-frontend.git (fetch)
origin  git@github.com:ingka-group-digital/pricera-frontend.git (push)
~/

# explicitly add a remote repo, required when creating the repo locally first and want to push changes to repo in github
$ git remote add [-t <branch>] [-m <master>] [-f] [--[no-]tags] [--mirror=(fetch|push)] <name> <URL>

$ git remote add origin git@github.com:User/UserRepo.git
$ git remote add origin git@github.com:ingka-group-digital/pricera-frontend.git

# change a remote repo's url `
git remote set-url origin git@github.com:User/UserRepo.git



# set current branch to track an upstream branch
$ git branch --set-upstream-to=RemoteBranchName LocalBranchName
$ git branch -u RemoteBranchName LocalBranchName


```

**How to Use Different Users/Accounts Push to Their Own Repos?**




```bash
```

```bash
```

```bash
```

```bash
```

```bash
```


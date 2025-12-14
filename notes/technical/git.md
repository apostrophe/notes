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


**Standard commands**
```bash
git push origin feature/CWEL-565-update-order-status
```


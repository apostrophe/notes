```bash
git config --list
git config --get credential.helper
git config set user.name "Ben Schilke2"


# enable verbose mode with ssh auth
git config core.sshCommand "ssh -v" # -v, -vv, -vvv
# disable
git config unset core.sshCommand

# specify specific key-pair
GIT_SSH_COMMAND='ssh -i ~/.ssh/keypair' git push origin master

```
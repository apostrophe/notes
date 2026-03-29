### Terminology
head_ref - source branch name?
base_ref - destination branch name?

branches
feature_branch (head_ref) -> main (base_ref)  

example of it used here:
/Users/benjamin.schilke/repos/pricing-operations/pricera-backend/.github/workflows/determine-changes.yml

### Config 
```bash
git config --list
git config --get credential.helper
git config set user.name "Ben Schilke2"
```

### Standard Commands
```bash
git pull --ff-only
git merge --rebase
git push origin feature/CWEL-565-update-order-status

git commit --amend --no-edit

# pull latest of main branch into local feature branch
git pull origin main --rebase
```

### Branches
```bash
git branch # list all local branches
git branch -r # list remote branches
git branch -a # list all branches (local and remote)
git branch -v # list remote branches verbose

```

### Stash
```bash
# stash individual files
git stash push -m "templates to add later" -- path/to/file1 /path/to/file2 /path/to/file3

# show details of stash (actual changes)
git stash show -p stash@{0}

git stash apply # applies the latest (stash{0})

# apply a specific stash:
git stash apply stash@{1}
```

### Reverting Changes
1. If you're going to be reverting a whole set of changes, helps to have them in a single commit. Consider squashing multiple commits.
2. Generally you can revert any commit by using the below, -n prevents git from committing your revert, so you can run this for multiple commits and then commit it all at once.
```bash
git revert -n {commit hash}
```
3. You can also do a range of commits (according to chatgpt api)
```bash
git revert -n 
```

### Logging/Verbose Mode

```bash
export GIT_TRACE=1
# or
GIT_TRACE=1 <   git command>

# also for troubleshooting ssh issues
GIT_SSH_COMMAND="ssh -vvv"

# others? https://stackoverflow.com/a/75978181
GIT_CURL_VERBOSE=true
GIT_TRACE_PACK_ACCESS=true
GIT_TRACE_PACKET=true
GIT_TRACE_PACKFILE=true
GIT_TRACE_PERFORMANCE=true
GIT_TRACE_SETUP=true
GIT_TRACE_SHALLOW=true
```


### Remote Repos and Branches
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

### Tracking a Branch   

```bash
If you wish to set tracking information for this branch you can do so with:

    git branch --set-upstream-to=origin/<branch> POPS-4980-2
```


### 2 accounts on Mac - Solution -> See Simpler Approach (below)
1. Deactivate ~/.ssh/config file (renamed to con_fig)
2. add to ssh-agent:
    `ssh-add --apple-use-keychain ~/.ssh/worklaptop-apostrophe-github-acct`
    view current list:
      `ssh-add -l`
3. run command with key explictly mentioned:
    `GIT_SSH_COMMAND='ssh -i ~/.ssh/worklaptop-apostrophe-github-acct' git push -u origin main`

### Simpler Approach
1. Give 'ikea' user account access to personal repo
2. Commit using this account

```bash
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
## Issues

remote branch has more recent updates:
```bash
$ git push origin <feature name>
To github.com:ingka-group-digital/pricera-backend.git
 ! [rejected]            POPS-4980-2 -> POPS-4980-2 (fetch first)
error: failed to push some refs to 'github.com:ingka-group-digital/pricera-backend.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```
remedy: `git pull origin <feature name>`


## How git Works

1. git takes the content of files in the repo, compresses them using Zlib, maps the contents of files to a hash and stores those compressed contents in .git/objects/xx/xxxxx where xx/xxxxx is the first 2 chars of the hash and then the rest of the hash
2. when adding these contents to the index/staging, a binary index file is updated  
3. when the changes are committed, the mapping of the commit, to a tree object and then to the blob objects can be found using the below command:  
`git cat-files -p <hash>`  
    a. enter the commit hash, and get a commit file that looks like this:
    ```
    tree 422b1e052083e26b8de9eabd1423ed22f8dbcaf4
    parent 8243f5755af54c0b01cd21de4c2094c7c32ad371
    author Ben Schilke <benjamin.schilke@ingka.ikea.com> 1772782629 +0100
    committer Ben Schilke <benjamin.schilke@ingka.ikea.com> 1772791876 +0100
    ```
    b. enter the tree hash and get a list of every file and folder found at the root:
    ```
    100644 blob 0c4d7f1165e8a123f2fcfe63ba9bbb66b14a66ca	file01
    100644 blob bceeb2c491c4bf2e1869637787897d33b45cf583	file02
    040000 tree c25c8e9e0af4fd73ca9e2c7ec012a2feebb6839d	folder01
    ```
    c. enter the hash of a blob object from the above file and get the contents of that blob (the hash of a blob object points to/returns contents of a file).  
    d. enter the hash of a tree object from the above file and get the contents of that directory (the hash of a tree object points to/returns contents of a directory)  
    -- this is important: this is how git can restore the state of hundreds of files based on a single commit hash -- 
    commit hash (a hash of the entire project) 
        -> tree object hash (all files and folders at the root) 
            -> tree object hashes -> contents of a folder
            -> blob object hashes -> contents of file

## Deep Dive
source: https://gemini.google.com/u/2/app/6a3c1b4dfd0c19de?pageId=none

Git Object Model
- think of git as a 2-way name-value data store
    - you give it content, it returns the hash of that content
    - you give it a hash, and it returns the associated content
- there are only 4 object types
    - blobs (binary large objects) - the content of your files, no filenames
        - 2 files with the exact same content will be stored in the same single blob
    - trees - is it fair to say they represent the file system
        - they map filenames to blob/hash
        - the map directories to filenames?
    - commits - a small file that points to 'a specific tree (the snapshot of the project at that point)' -- so a tree represents a point in time?
    - tags - a persistent pointer to a specific commit, often used for versioning


```bash
cd /Users/benjamin.schilke/repos/sandbox/git/deep-dive/lesson01
#git init
# create a hash of this string and create the associated files in .git
echo "Learning Git Internals" | git hash-object -w --stdin

# view the files created from the above command
find .
# view the contents associated with the hash
git cat-file -p [YOUR_HASH_HERE]
```

SHA Hash - Git's Fingerprint
- a hash has a 1-1 maps to content
- the hash is also it's location


a crack at how content maps to a hash, then trees are content+filesystem info mapped to a hash, then a commit is a grouping of the above plus a small file hashed
```text
file01
'file contents, etc.' - 

'file contents, etc.' <-> hash <-> tree

experiments: `/Users/benjamin.schilke/repos/sandbox/git/deep-dive/lesson01`
```

`git init`
- creates .git directory
- most important
    - `objects/` - where blobs, trees and commits are stored
    - `refs/heads/` - where branch pointers live
    - `HEAD` - a file that contains `ref: refs/heads/main`, which indicates the branch you're pointing to


```bash
```

```bash
```

```bash
```



```bash
# text search
grep -rl "insert into waitwhile_visit" ~/Library/DBeaverData/ | less

# mac: open a folder in finder
open /path/to/folder
# linux/mint desktop
nemo .

# set env variable
export NEXT_PUBLIC_PUP_APP_DEV=true
unset NEXT_PUBLIC_PUP_APP_DEV

echo $NEXT_PUBLIC_PUP_APP_DEV



# what service is using port x?
lsof -i:5432 | grep LISTEN

# ps aux --forest equivalent
pstree | less
```


what services
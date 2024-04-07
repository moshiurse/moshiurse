To see manual of any comman. Just type man ls/mkdir/rm etc
```
man ls
```
press q to quit
CTRL + F to go page by page
g to go begginning
G to go end of document
to search anything /search_query and navigate using n , SHIFT + n to go upper

Check the actual path of cmd or which type of command
```
type apt
```

get help 
```
help cd
```

Some are not working like ls use instead
```
ls --help
```

if ifconfig is  not found install net-tools
```
sudo apt net-tools
```

check manual ifconfig
```
man -k ifconfig
```
simmilar tolls is  apropos
```
 apropos ifconfig
```
The df command displays information about total space and available space on a file system
```
df
```

For clear the screen shortcut 
```
CTRL + L
```

CTRL + D to exit shell
CTRL + A for go to beginning of a command
CTRL + E for go to end of a command
Ctrl + U	Delete from the cursor to the start of the line.
Ctrl + Z	Pause the current process (can be resumed).

bg %1 to resume again

To Show bash history(Store after logout)
```
cat .bash_history
```
Ordered History
```
history
```
Excute nth history
```
!17
```
Execute last 5th command
```
!-5
```
Show history time also - set the time format
```
HISTTIMEFORMAT="%y-%m-%d %T --> "
```
Now check the history

### Sudo root users
```
sudo su
```
Check user usergroup using id
```
id
```
to logout 
```
exit
```
Go to root as root user
```
sudo su - 
```
directory changed to /root
```
pwd
```
Look the # for root user instead of $

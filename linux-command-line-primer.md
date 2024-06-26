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

add user
```
sudo useradd deploy
```
Change root password
```
sudo passwd root
```

### Linux Filesystem

to home directory
``` 
ls ~ 
```
this commands simmilar to 
```
ls /home/user/
```
```
ls /root
```
Error: ls: cannot open directory '/root': Permission denied

```
sudo /root
```

## Linux Directory Structure Breakdown

Here's a breakdown of the essential directories in a Linux system:

**Essential Directories**

* **/bin:**  This directory stores essential executable programs (commands) used by all users in the terminal, like `ls`, `mount`, and `rm`.
* **/boot:**  This directory contains crucial files needed for system startup, including the Linux kernel, a RAM disk image, and bootloader configuration files.
* **/dev:**  This directory houses device files, which act as special entries representing physical hardware devices like hard drives.
* **/etc:**  This directory holds system-wide configuration files that influence the overall system behavior for all users.
* **/home:**  Consider this your "home sweet home" directory. It stores user-specific home directories.
* **/lib:**  This directory contains essential dynamic libraries and kernel modules required by the system for various functionalities.   
* **/media:**  This directory serves as a mount point for external devices like hard drives or removable media (floppies, CDs, DVDs). 
* **/mnt:**  Similar to **/media**, this directory is also used for mounting devices, but it's specifically dedicated to "temporarily mounted" devices like network filesystems.  
* **/opt:**  This directory offers storage for additional software not managed by the package manager.   
* **/proc:**  This virtual filesystem provides a communication channel for the kernel to send information to processes.  
* **/root:**  This directory serves as the superuser's (administrator) home directory. It's separate from **/home** to ensure system booting even if **/home** is unavailable.  
* **/run:**  This directory is a temporary filesystem (tmpfs) accessible during the early boot process. It stores ephemeral runtime data that gets removed or truncated at boot. It replaces various legacy locations like **/var/run**, **/var/lock**, etc., which were previously used for temporary data.  
* **/sbin:**  This directory contains crucial administrative commands typically used only by the superuser for system administration.   
* **/srv:**  This directory can house data directories for various services, such as HTTP (often at **/srv/www/**) or FTP.  
* **/sys:**  This virtual filesystem provides access to set or retrieve information about the system's hardware as perceived by the kernel.  
* **/tmp:**  This directory serves as a storage location for temporary files used by applications.  
* **/usr:**  This directory contains the majority of user utilities and applications. It partially mirrors the root directory structure, including subdirectories like **/usr/bin** and **/usr/lib**.  
* **/var:**  This directory is dedicated to variable data that persists across reboots, such as logs, databases, websites, and temporary spool files (e.g., email). A notable subdirectory here is **/var/log**, which stores system log files.


To get cpu info
```
cat /proc/cpuinfo
```

### ls command

**ls [options] [FILE]**

```
ls
```
```
ls /var
```
**Show details**
```
ls -l /var
```
**Show details with human readable(see the file size)**
```
ls -lh /var
```
**Getting hidden directory**
```
ls -la
```

**Sort**
```
ls -lhS /var
```
```
ls -l -X /etc/
```
**To hide certain file**
```
ls --hide=*.conf /etc
```

**To go through recuirsively**
```
ls -lR /etc
```

**To get directory size**
```
sudo du -sh /etc
```
**Understanding File Permissions (lrwxrwxrwx):**

The string `lrwxrwxrwx` is composed of two parts:

* **File Type (l):** The first character, `l`, indicates the file type. In this case, `l` stands for a **symbolic link (symlink)**. A symlink acts like a shortcut, pointing to another file or directory on the system.

* **File Permissions (-rwxrwxrwx):** The remaining characters represent access permissions for three user groups:

    * **Owner Permissions (rwx):** The first set of three characters (here, `rwx`) define the permissions for the **owner** (the user who created the symlink). These permissions can be:
        * `r` (read): Allows the owner to read the contents of the symlink (or the target file/directory it points to).
        * `w` (write): Allows the owner to modify the symlink itself (not the target).
        * `x` (execute): Allows the owner to follow the symlink and access the target file/directory.
    * **Group Permissions (rwx):** The second set of three characters defines permissions for the **group** that owns the symlink. These permissions follow the same meaning as owner permissions: `r` (read), `w` (write), and `x` (execute).
    * **Other Users Permissions (rwx):** The final set of three characters defines permissions for **all other users** on the system. Similar to owner and group permissions, these can be: `r` (read the symlink), `w` (not applicable for symlinks), and `x` (follow the symlink).


### File timestamp
```
stat /etc/passwd
```

```
Access: 2024-04-08 04:53:27.542362287 +0600
Modify: 2024-04-08 04:53:27.492362285 +0600
Change: 2024-04-08 04:53:27.492362285 +0600
Birth: 2024-04-08 04:53:27.492362285 +0600
```

```
ls -lt //modification time
ls -lu //access time
ls - lc //change
ls -l --full-time
```

### View File

**Cat**

```
cat file1
```
view Multiple files
```
cat file1 file2
```
View with number of lines
```
cat -n /etc/passwd
```
concatenete multiple files
```
cat /etc/hosts /etc/host.conf > my_host.txt
cat my_host.txt
```

**cat has limitation. text exceeds window cannot be viewed**
Use **more** or **less**

to see realtime or watch a file
**tail** used for to see from end
**head** used for to see from start
default line is 10
```
tail -f /var/log/auth.log
```

To see specific line number 
```
head -n 20 /var/log/auth.log
```
to see any changes to file or text use **watch**
```
watch ls
```
after 3 sec
```
watch -n 3 -ls -l
```
```
watch -1 -d ifconfig
```
It will update and highlight real time if any file added or deleted 

Creating file with touch
```
touch sample.txt 
```

creating folder with mkdir
```
mkdir dir
```
with logs
```
mkdir -v dir2
```
multiple directory at a time
```
mkdir dir3 dir4
```
If you want to create a directory where parent is not exists
```
mkdir -p first/second/third
```
see the structure
```
tree first
```

Copy file using **cp**
```
cp file1 file2
```
Cp created file if not exists. Overriden file if already exists.

if you want to prompt overriden message 
```
cp -i file1 file2
```

copy multiple files to folder
```
cp file1 file2 dir1/
```
copy a directory full contents recuirsively
```
cp -r dir1/ dir2/
```
copy file using -p to own same user
```
cp -p file1 dir2/
```
**Moving and renaming file and directory**
```
mv dir1/file1 dir2/
```

multiple file at once
```
mv file1 file2 dir2/
```
move all txt files to a folder
```
mv dir1/*.txt dir2/
```

replace a file with another happenned if file has same name
if dir2 has already a.txt it will replace.
```
mv dir1/a.txt dir2/
```

To get warning use -i
```
mv -i dir1/a.txt dir2/
```
```
mv -n dir1/a.txt dir2/
```
```
mv -u dir1/a.txt dir2/
```
to rename
```
mv dir1/a.txt dir/abc.txt
```
move and rename 
```
mv dir1/a.txt dir1/dir2/aa.txt
```

**Removing file and folder**

```
rm a.txt b.txt
```
to delete directory use -r
```
rm -r a/
```

use f for force remove in case of permission problem
```
rm -rf a/
```

### Using Pipe

command combining with head to show latest ordered data
```
ls -lSh /etc/ | head
```
getting 20th item from list
```
ls -lSh /etc/ | head -n 20 | tail -n 1
```
Getting auth info with auth failure
```
cat -n /var/log/auth.log | grep -a "authentication failure"
```
Getting total line number count
```
cat -n /var/log/auth.log | grep -a "authentication failure" | wc -l
```

### Command redirection

```
ls -l > ls.txt
```
```
cat ls.txt  
```
now add another
```
ifconfig > ls.txt
```
It will overridden the previous. to avoid this **>>**
```
ifconfig >> ls.txt
```

to show error
```
tail -n 3 /etc/shadow 2>>error.txt
```
```
cat error.txt
```
tail: cannot open '/etc/shadow' for reading: Permission denied

Show normal output and error output 
```
tail -n 2 /etc/passwd /etc/shadow > output.txt 2>>error.txt
```
Show all in one file
```
tail -n 2 /etc/passwd /etc/shadow > output.txt 2>&1
```
using **cut** filter 
```
ifconfig | grep ether | cut -d" " -f10 > mac.txt
```
now you can see your mac address
```
cat mac.txt
```

conmbine output and save to file using **tee**
```
ifconfig | grep ether | cut -d" " -f10 | tee mac2.txt
```

by default tee overriden previous. to avoid use flag -a
```
who | tee -a mac2.txt
```

output to multiple file
```
uname -r | tee -a mac.txt mac2.txt
```

### Finding files and directories

**mlocate**

```
 sudo apt install mlocate
```
```
sudo updatedb
```
```
ls /var/lib/mlocate
```

```
locate -S 'shadow'
locate -b 'shadow'
locate -b '\shadow'
locate -e 'shadow'
locate -i RainShadow
locate -b -r 'regexPattern'
```

**which**

```
which ls
which pwd
which -a find
which pwd ls find
```

**find**
```
find . -name ab.txt
find . -iname Ab.txt
find . -name ab.txt -delete
```
There is many more options with find

**Find and execute**

```
sudo find /etc -type f -mtime 0 -exec cat {} \;
```
prompt for every file
```
sudo find /etc -type f -mtime 0 -ok cat {} \;
```
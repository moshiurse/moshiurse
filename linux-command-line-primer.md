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
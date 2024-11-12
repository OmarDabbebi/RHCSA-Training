<h1 align="center">Red Hat Enterprise Linux System Administration</h1>

## Introduction
Welcome to this course on System Administration under Red Hat Enterprise Linux.
This course is designed to prepare you for the RHCSA (Red Hat Certified System Administrator V9) exam!

## Table of Contents
- [Installation of Red Hat Enterprise Linux & Registration](#-I.-Installing-Red-Hat-Enterprise-Linux-&-Registration)
- [Basic Commands & Shell Scripts](##-II.-Basic-Commands-&-Shell-Script)
- [User and Group Management](##-III.-User-and-Group-Management)
- [Task Automation](##-IV.-task-automation)
- [Service Management](##-V.-Service-Management)
- [Archiving & Compression](##-VI.-Archiving-&-Compression)
- [NFS & AutoFS](##-VII.-NFS-&-AutoFS)
- [Storage Management](##-VIII.-Storage-Management)
- [Container Management](##-IX.-Container-Management)
- [BaseOS & AppStream Repositories](##-X.-BaseOs-&-AppStream-repositories)
- [Networks](##-XI.-Networks)
- [Root Password Reset](##-XII.-Root-Password-Reset)

## I. Installing Red Hat Enterprise Linux & Registration
### 0. VM Link
[Download RHEL 9 VM](https://www.mediafire.com/file/mjs6r2sb7oqrqzk/RedHat_9.1.1_64-bit.zip/file)

### 1. Create an Account on Red Hat
To start, you need to create an account on the official Red Hat website.
- Go to [redhat.com](https://www.redhat.com).
- Click on "Register" and follow the instructions to create your account.

### 2. Register on Red Hat Developers
Next, sign up as a developer on the Red Hat Developers site to access the Red Hat Enterprise Linux image.
- Visit [developers.redhat.com](https://developers.redhat.com).
- Create an account or log in if you already have one.

### 3. Download the Red Hat Enterprise Linux Image
Download the ISO image of Red Hat Enterprise Linux from the developers' site.
- Visit [this link](https://developers.redhat.com/products/rhel/download) to download the image.

### 4. Register Your System
Once Red Hat Enterprise Linux is installed, you need to register your system to access updates and software.
- Open a terminal and run the following command:
```bash
subscription-manager register
 ```

## II. Basic Commands & Shell Script
### Basic Commands
- `pwd`: Displays the current directory path.
- `cd directory`: Changes the current directory to "directory".
- `cd ..`: Moves to the parent directory.
- `ls`: Lists files and directories in the current directory.
- `ls -l`: Lists detailed information about files and directories.
- `ls -a`: Lists all files, including hidden ones.
- `whoami`: Displays the current user's name.
- `touch file`: Creates a new file.
- `mkdir dir`: Creates a new directory.
- `mkdir -p`: Creates directories recursively, including parent directories.
- `cat`: Displays the content of a file.
- `echo "text"`: Outputs text to the screen.
- `echo "text" > file`: Overwrites a file with the specified text.
- `echo "text" >> file`: Appends text to the end of a file.
- `command 2> file`: Redirects error output to a file.
- `vim / nano`: Edits a file using the Vim or Nano editor.
- `rmdir`: Removes an empty directory.
- `rm`: Deletes a file.
- `rm -rf`: Recursively and forcibly deletes a directory.
- `man / help`: Provides information about a command.
- `ctrl + a`: Moves the cursor to the beginning of the line.
- `ctrl + e`: Moves the cursor to the end of the line.
- `ctrl + c`: Stops the execution of a command.
- `history`: Displays the command history.
- `cp -rf sourceLocation destinationLocation`: Copies a directory.
- `cp sourceLocation destinationLocation`: Copies a file.
- `mv sourceLocation destinationLocation`: Renames or moves a file or directory.
- `grep`: Searches for patterns in a file.
- `grep -w`: Searches for an exact word.
- `find`: Searches for files and directories within a directory.  
  **Syntax**: `find directory [options] [-exec cp -a {} destination \;]`  
  **Options**:  
  - `-name`: File name,  
  - `-group`: Group owner,  
  - `-user`: Owner,  
  - `-size`: Size `n{k,M,G…}`, `+n{k,M,G…}`, or `-n{k,M,G…}`,  
  - `-perm`: Permissions,  
  - `-type`: `f` for file and `d` for directory.  

  **Command**:  
  `cp`: Copies the found files and directories (`cp -a {}`).
### Shell Script
- The file should have a `.sh` extension (indicates that the file is a shell script).
- It must start with a shebang: `#!/bin/bash` or `#!/bin/sh` (indicates to the system which interpreter to use for executing the script).
- Display text: `echo "text"`
- Input a variable: `read variable`
- Call a variable: `$variable`
- Environment variable for the current user's home directory: `$HOME`
- Environment variable for the current user's username: `$USER`
- Environment variable that shows the current user's ID: `$UID`
- Environment variables for the current date and time: `date`
- Log messages to the system log: `logger "text"`
- Check system log text: `journalctl | grep "text"`
- To execute scripts: `bash file.sh` or `sh file.sh`,  
  or use `chmod +x file.sh` followed by `./file.sh`.

  #### Example of a script called example.sh.

```bash
vim example.sh
#! /bin/bash
echo “Please provide your name”
read name
echo “hello $name”
logger “user $name executed the greeting script”
bash greeting.sh
journalctl | grep user 
```

## III. User and Group Management
### Important Files

- **/etc/shadow**: Contains the passwords.
- **/etc/passwd**: Contains user information.
- **/etc/group**: Contains groups.
- **/etc/skel**: Template for user home directories.
- **/etc/login.defs**: Contains user creation parameters.
- **/etc/default/useradd**: Contains default user values.
- **~/.bash_profile** & **~/.bashrc**: Used to add user-specific variables.
- **/etc/security/pwquality.conf**: Used to change password characteristics (root access required).

### Useful Commands

- `su user`: Switches to the specified user.  
- `su - user`: Switches to the specified user and changes to their home directory.  
- `sudo`: Execute a command with root privileges.  
- `useradd [option] username`: Add a new user.  
- `passwd username`: Assign a password to the user.  
- `useradd -M username`: Add a user without a home directory.  
- `chage [option] username`: Manage password settings.  
- `chage -d 0 username`: Force a password change on next login (Last password change date = 0 days).  
  **Options**:  
  - `-m`: Minimum number of days before a user can change their password.  
  - `-M`: Maximum number of days before the password expires.  
  - `-E`: Exact expiration date (yyyy-mm-dd).  
  - `-W`: Number of warning days before expiration.  

- `usermod [option] username`: Modify user properties.  
  **Options**:  
  - `-u`: Change UID.  
  - `-g`: Change primary GID.  
  - `-G`: Change secondary groups.  
  - `-aG`: Add to an additional secondary group.  
  - `-c`: Add a comment.  
  - `-s`: Change the shell.  
  - `-d`: Change the home directory.  

- `usermod -s /sbin/nologin username`: Make a user inactive.  
- `usermod -L username`: Lock a user's account by disabling their password.  
- `usermod -U username`: Unlock a user's account.  
- `echo "username ALL=(ALL) ALL" >> /etc/sudoers`: Grant sudo privileges to a user.  
- `echo "username ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers`: Grant sudo privileges without requiring a password.  
- `groupadd [option] groupname`: Add a new group.  
- `groupmod [option] groupname`: Modify a group.  
- `groupadd -o -g 490 groupname`: Assign an already used GID.  
- `usermod -g groupname`: Assign a user to a primary group.  
- `usermod -G groupname`: Assign a user to a secondary group.  
- `usermod -aG groupname`: Add a user to an additional secondary group.  
- `groups username`: Display the groups of a user.  
- `userdel username`: Delete a user.  
- `userdel -r username`: Delete a user and their home directory.  
- `groupdel groupname`: Delete a group.  
- `chown [options] [newowner][:newgroup] filename`: Change the owner and group of a file.  
  - `-R`: Apply recursively to a directory.  
- `chown newowner filename`: Change the owner of a file.  
- `chown :newgroup filename`: Change the group ownership of a file.  

### User permissions  
read – write – execute  
r   w   x  
2^2  2^1  2^0  
4    2    1 → in octal form  
user    group  others  
u       g      o → in symbolic form  
7   7   3 → example  
`man chmod`

- `chmod [options] permission filename`: Modify file permissions.  
  Example:  
  - Owner: read and write  
  - Group: read, write, and execute  
  - Others: read  
  - Octal mode: `chmod 674 filename`  
  - Symbolic mode: `chmod u=rw,g=rwx,o=r filename`  
  - Add execute for user: `chmod u+x filename`  
  - Remove execute for group: `chmod g-x filename`  
  - `0666` → Maximum permission for a file  
  - `0777` → Maximum permission for a directory  
  - `0022` → Default Umask value  

- `umask new_value`: Temporarily modify the umask value.  
- `echo "umask new_value" /etc/login.defs`: Permanently modify the umask; it will apply to all users when they log into the system.  
- `echo "umask new_value" ~/.bashrc`: Permanently modify the umask for a specific user when they log into the system.  

Maximum permission (777) - mask = default permission  
mask = maximum permission (777) - default permission  

### Special Permissions:  
- **SUID (Set User ID)**: 4000  
  - `(rws --- --- for rwx --- ---), (rwS --- --- for rw- --- ---)`  
  When SUID is applied to a file or command, it is executed with the permissions of the file's owner whenever any user runs it.  
  Example of a command with SUID: `passwd`  
  `chmod u+s filename` → Apply SUID to a file.  

- **SGID (Set Group ID)**: 2000  
  - `(--- rws --- for --- rwx ---), (--- rwS --- for --- rw- ---)`  
  When applied to a directory, all newly created files in the directory will inherit the group ownership of the directory.  
  `chmod g+s dirname` → Apply SGID to a directory.  

- **Sticky Bit**: 1000  
  - `(--- --- rwt for --- --- rwx), (--- --- rwT for --- --- rw-)`  
  When applied to a directory, it prevents users (other than the owner and root) from deleting files within the directory.  
  `chmod o+t dirname` → Apply Sticky Bit to a directory.  

## IV. Task Automation

### Main Commands:
- `crontab -e`: Edit the crontab for the currently logged-in user.  
- `crontab -e -u username`: Edit the crontab for a specific user.  
- `cat /etc/crontab`: View the current configuration details.

### Time Intervals:
- `@hourly`: Every hour.  
- `@daily`: Every day.  
- `@weekly`: Every week.  
- `@monthly`: Every month.  
- `@annually`: Every year.  
- `@reboot`: At every reboot.

### Notes on Intervals:
- `x,y`: x and y.  
- `x-y`: From x to y.  
- `x-y/z`: From x to y with a step of z.  
- `*`: Every unit.  
- `*/z`: Every z units.

## V. Service Management

### SSHD Service:
#### Theory:
In simple terms, SSH allows a user to securely connect to another computer as if they were physically in front of it. It uses strong cryptography to secure the communication between the two machines, meaning the exchanged data, including credentials and commands, are protected against interception.  
**Note:** Well-known ports are numbered from 0 to 1023, and they are associated with standardized services like HTTP (port 80) and SSH (port 22).

#### Practice:
##### Connecting to another machine via SSH using a password:
- `dnf install openssh-server` → Install the SSH server (machine as SSH server).
- `systemctl enable sshd`  
- `sudo systemctl start sshd` → Start and enable the SSH service (machine as SSH server).
**Note:** Each service on Red Hat has two layers of security by default: the firewall (`Firewalld`) & `SELinux` (Security-Enhanced Linux).
  
- `firewall-cmd --add-port=22/tcp --permanent`  
- `firewall-cmd --reload`  
- `firewall-cmd --list-ports` → Open the SSH port for incoming connections on machine B (as SSH client).
- `ssh username@server_ip_address` → Test SSH connection (machine as SSH client). The user must have a password.
Or  
- `vim /etc/hosts`  
`client_address hostname` → Set a hostname for the IP address of each machine.  
- `ssh user_client@hostname`  
##### Connecting to another machine via SSH without a password:
To allow a passwordless connection, you need to generate and configure SSH keys on machine (B) and add them to the other machine (server). This will allow the server to recognize and permit connections from machine B.  
- `ssh-keygen -t rsa` → Generate SSH keys (on the machine wanting passwordless connection).
- `ssh-copy-id user@server_machine` → Copy the public key from Machine B to Machine A and add it to the `authorized_keys` file in the `.ssh` directory of the user on Machine B (`/home/username/.ssh/authorized_keys`).
- `ssh user@server_machine`  
##### Connecting to another machine using a port other than 22:
By default, SSH uses port 22, but it can be changed:
**Server-side:**
- `vim /etc/ssh/sshd_config`  
`port 2222` → Change port from 22 to 2222.  
- `man semanage port`  
`semanage port -a -t ssh_port_t -p tcp 2222` → Add the new port to SELinux (2222).  
- `firewall-cmd --permanent --add-port=2222/tcp`  
- `firewall-cmd --reload` → Add port to the firewall.  
- `systemctl restart sshd` → Restart the service.  
**Client-side:**
- `ssh user@server_address -p 2222` → Connect using the new port.

### HTTPD Service:
#### Theory:
The web server stores all files necessary for delivering a website's content, including files for static pages and applications for dynamic pages. The role of the web server is to serve these files and manage interactions between the user’s browser and the website’s resources.  
A HTTP (GET) request is like a command to the server to get a specific file (e.g., "index.html"), and the HTTP response is how the server replies, sending back the requested content (the HTML file in this case).

- `/var/www/html` is a common directory path for storing files served by a web server.
- `"index.html"` (/var/www/html/index.html) is an HTML file that serves as the homepage or starting point for a website.

#### Practice:
- `dnf install httpd`
- `systemctl enable --now httpd` → Install and enable the service.
- `systemctl status httpd` → Check if the service is active.
- `echo "bnj" >> /var/www/html/index.html`
- `firewall-cmd --permanent --add-service=http`
- `firewall-cmd --permanent --add-service=https`
- `firewall-cmd --reload` → Add HTTP and HTTPS to firewall rules.  
After placing an `index.html` file in `/var/www/html`, and if the web server is running, accessing the server's IP address or domain in a web browser will display the contents of `index.html`.
- `dnf install curl`
- `curl http://@server/index.html`  
(If not working, try: `chown apache:apache /var/www/html/index.html`)

#### Changing port 80 to `<new_port>`:
- `vim /etc/httpd/conf/httpd.conf`  
`listen <new_port>`
- `man semanage port`  
`semanage port -a -t http_port_t -p tcp <new_port>` → Add the new port to SELinux.
- `firewall-cmd --permanent --add-port=<new_port>/tcp`  
- `firewall-cmd --reload` → Add the new port to the firewall.
- `systemctl restart httpd` → Restart the service to apply the new configuration.
- `curl localhost:<new_port>/index.html` → Verify the new port.

#### Changing the default directory from `/var/www/html` to `/var1/web/html`:
- `vim /etc/httpd/conf/httpd.conf`  
`DocumentRoot "/var1/web/html"`  
`<Directory "/var1/web">`  
    `AllowOverride None`  
    `Require all granted`  
`</Directory>`  
`<Directory "/var1/web/html">`
- `man semanage fcontext`
`semanage fcontext -a -t httpd_sys_content_t "/var1/web/html(/.*)?"`  
`restorecon -R -v /var1/web/html/`
- `echo "hello2" >> /var1/web/html/test.html`
- `systemctl restart httpd`
- `curl localhost/test.html` or `curl http://@iphost/test.html`  
(If not working: `chown -R apache:apache /var1`)

### NTP Service:
#### Theory:
An NTP server is a server that provides the accurate time to client computers on a network. It maintains a precise clock by regularly synchronizing with accurate time sources, such as atomic time servers or GPS. The NTP server responds to client requests to provide the current time with high precision.

#### Practice:
**Server-side: Allow client access to time:**
- `dnf install chrony`
- `systemctl enable chronyd`
- `systemctl start chronyd` → Install and enable the service.
- `vim /etc/chrony.conf`  
`allow @client_ip`  
- `systemctl restart chronyd`  
- `firewall-cmd --add-service=ntp --permanent`  
`firewall-cmd --reload`

**Client-side: Access to time:**
- `dnf install chrony`
- `systemctl enable chronyd`  
- `systemctl start chronyd` → Install and enable the service.
- `vim /etc/chrony.conf`  
`server @server_ip iburst`  
- `systemctl restart chronyd`  
- `chronyc sources -c` → Check sources.

To enable NTP:
- `timedatectl set-ntp true`  
- `timedatectl`

Set a time zone:
- `timedatectl list-timezones`  
- `timedatectl set-timezone <zone>`  
- `timedatectl`

## VI. Archiving & Compression

- `tar -cvf archivename.tar répertoire` → Combine files into a single large file called an archive. (Step 1)
- `tar -tvf archivename.tar` → List the contents of an archive.
To compress the large file obtained using gzip or bzip2: (Step 2)
- `gzip archivename.tar` → Compress an archive with gzip.
- `gzip -d archivename.tar.gz` → Decompress an archive with gzip.
- `bzip2 archivename.tar` → Compress an archive with bzip2.
- `bzip2 -d archivename.tar.bz2` → Decompress an archive with bzip2.
You can do both steps simultaneously (archiving + compression):
- `tar -cvzf répertoire.tar.gz répertoire` → Archive and compress a directory into gzip.
- `tar -cvjf répertoire.tar.bz2 répertoire` → Archive and compress a directory into bzip2.
- `ls -lh` → Check the size of the file.

## VII. NFS & AutoFS
### NFS: 

#### théorie:    

**file server?**  
Un ordinateur responsable du stockage afin que d'autres ordinateurs du même réseau puissent accéder aux fichiers, via Network share: NFS (protocol of Network share in linux).  

**how to use NFS service?**  
The server exports the directory, then the client mounts the NFS filesystem.  

Any service has a layering protection:  
- **firewall**; firewalld-cmd command (default: rules are blocked)  
- **selinux**; semanage command (security enhanced linux)  

#### pratique:  
**Partie serveur:** (must be root: su -)
- `dnf install nfs*` → Install the service.
- `systemctl enable --now nfs-server` → Enable and start the service.  
  (or `systemctl enable nfs-server` then `systemctl start nfs-server`)  
- `systemctl status nfs-server` → Verify the status of the service

**configuration?**
- `mkdir /shared_directory` → Create the directory to share.
- `echo “/shared_directory @ipclient(x,y)” /etc/exports` → Configure the shared directory on the server.  
  `x` can be `ro` or `rw` & `y` can be `no_root_squash` or `async`  
  - `no_root_squash` → The superuser of the client retains full privileges on shared files.  
  - `root_squash` → (default) The client's privileges are limited even for the superuser.  
  - `rw` → The shared directory will be readable and writable for the client.  
  - `ro` → The shared directory will be just readable for the client.  
  - `sync` → (default) Synchronous connection; the server waits for data to be physically written to disk before responding to client's write request.  
  - `async` → Asynchronous connection; the NFS server can respond to the client before data is physically written to disk.  

- `systemctl restart nfs-server` → Restart the service because we modified its configuration file (`/etc/exports`)
- `semanage boolean -l | grep nfs_export_all_ro` → Verify that NFS is allowed to export with ro mode: must be on.
- `semanage boolean -l | grep nfs_export_all_rw` → Verify that NFS is allowed to export with rw mode: must be on.
- `setsebool -P nfs_export_all_rw=1` → Allow sharing with rw mode.
- `setsebool -P nfs_export_all_ro=1` → Allow sharing with ro mode.
- `firewall-cmd --list-all` → To see enabled services.
- `firewall-cmd --add-service=nfs --permanent` → To allow NFS service.
- `firewall-cmd --reload` → To reload firewall rules.
- `exportfs -avr` → To export the directory to the client.

**Partie client:** (must be root: su -)
- `dnf install nfs-utils` → Install the service.
- `mkdir /mount_point` → Create the directory where you will mount the shared directory.
- `mount -t nfs -o rw @ipserver:/shared_directory /mount_point` → Mount the shared directory.  
  (`umount /shared_directory` → To unmount the shared directory)
- `echo “@ipserver:/shared_directory /mnt/mount_point nfs _netdev 0 0” >> /etc/fstab` → Mount the shared directory permanently.
- `mount -a` → To execute the `/etc/fstab`
- `df -h` → To verify.

### AutoFS: 

#### théorie:  

**Autofs?**  
On-demand NFS or automatic mounting of shared directories.  
Autofs allows automatic mounting of filesystems, such as NFS shares, when users access specific directories. This helps optimize system resources by mounting filesystems only when necessary.  

- **server** → Exports.
- **client** → Auto mount (`auto.master` & `auto.misc`).

**Use case**: To share the home directory (server-side) so users can access it when they create a session (client-side).

Create a user named `john` on the two machines with UID 2001. His home directory on the server is named `/host/john`. It will be mounted on `/host/john` with Autofs when john connects.

**Note**: The user on the server must have a base directory, the client must not have the directory (for testing).

**Partie serveur:**
- `dnf install nfs*`
- `useradd -u 2001 -b /host john` → Create the base directory for the user on the server.
- `echo “/host *(rw,no_root_squash)” >> /etc/exports` → Modify the configuration file to export the base directory.
- `firewall-cmd --add-service rpc-bind --permanent`
- `firewall-cmd --add-service mountd --permanent`
- `firewall-cmd --add-service nfs --permanent`  
  Or just:  
  `firewall-cmd --add-service={rpc-bind,nfs,mountd} --permanent`
- `firewall-cmd --reload` → Add necessary services for automatic mounting.
- `exportfs -arv` → Export the base directory.

**Partie client:**
- `dnf install nfs-utils`
- `dnf install autofs` → Install necessary packages.
- `useradd -M -u 2001 -d /host/john john` → Create a user without a home directory.
- `echo “/host /etc/auto.misc” >> /etc/auto.master`
- `echo “john -rw @ipserver:/host/john” >> /etc/auto.misc` → Configure automatic mounting of the home directory.
- `systemctl restart nfs-server`
- `systemctl restart autofs`

## VIII. Storage Management
### Disks & Partitions:  

- **Partitioning**: Create one or more independent storage zones.
- **Disk Organization with MBR**: Maximum 4 partitions: 4 primary partitions and one extended partition that can contain several logical partitions.
- **Example**:  
  For SATA devices:  
  `/dev/sda` refers to the first SATA disk.  
  `/dev/sdb` refers to the second SATA disk...  
  `/dev/sda1` refers to the first partition on the first SATA disk.  
  `/dev/sda2` refers to the second partition on the first SATA disk...  
- **File System Formats**: This is how Linux organizes and stores files on a storage device: ext2, ext3, ext4, jfs, xfs, etc.  
- **Mounting**: Integrates a file system into the directory structure. Once you've mounted the disk, you can navigate its files as if they were part of your main computer.  
- **SWAP Partition**: A swap partition on a hard drive acts as a temporary storage space used by the operating system to move inactive data from RAM (memory) to disk.  
- `lsblk` → To see the disks and partitions.  
- `fdisk /dev/disk_name then n (new)` → To create a partition.  
- `mkfs.filesystem_name /dev/partition_name` → To format a partition.  
- `mkdir /mount_point` → To create the mount point.  
- `blkid /dev/partition_name` → To display the UUID of the partition.  
- `echo “UUID=uuid_of_the_partition		/mount_dir	xfs		defaults	0 0” >> /etc/fstab`  
  Then  
- `mount -a` → To mount the partition (permanent).  
  To remove a mounted partition:  
  **Note**: You must unmount before deleting a partition.  
  Remove the line from `/etc/fstab` if it’s mounted permanently, then run `mount -a`.  
- `umount partition_name`.  
- `fdisk /dev/disk_name then d (delete) then w` → To delete a partition.  
  **Note**: You must unmount before changing the partition type (for example, to swap).  
  To create a SWAP partition (create a partition and then change its type to swap):  
- `fdisk /dev/disk_name then t (change type), L (list all hex codes), choose the code for swap: 82, w (write)` → To change the type to swap.  
- `mkswap /dev/partition_name` → To format a SWAP partition.  
- `free -m` → To check SWAP.  
- `echo “uuid_of_the_SWAPpartition	none	swap	defaults	0 0” >> /etc/fstab then swapon -a` → To mount the partition (permanent).  
- `swapoff -a` → To disable swap.  

### Logical Volume Management (LVM)

To obtain a logical volume, you must:  
- Have a physical volume (PV) from a partition.
- Create a volume group (VG) from physical volumes (PV).
- Create a logical volume.

**Why**? (We need a 8GB volume, and we only have smaller partitions; the solution: use the concept of LVM).

**Note**: By default, when creating the VG, a small percentage will be reserved for metadata (one PE for each partition (PV)).

#### Creating an LV with an exact size:
- `pvcreate /dev/partition_name` → To create a physical volume.
- `vgcreate vg_name /dev/partition_name1 /dev/partition_name2…` → To create a volume group.
- `lvcreate -L size_unit -n lv_name vg_name` → To create the logical volume.

**Mounting the logical volume**:
- `mkdir /mount_point` → To create the mount point.
- `mkfs.xfs /dev/vg_name/lv_name` → To give a file system and format the LV.
- `echo “/dev/vg_name/lv_name	/mount_point	xfs	defaults	0 0” >> /etc/fstab then mount -a` → To mount the LV.

You can also extend the LV: there are two cases: when the VG has enough space and when the VG doesn't have enough space.

##### If the VG has enough space:
- `vgs` → To see the details of the VG (free size).
- `lvextend -r -L +<size> /dev/group_name/lv_name` → To extend the LV.
- `lvs` → To verify.

##### If the VG doesn’t have enough space: (extend VG then LV)
- `vgs` → To see the details of the VG (free size).
- `pvs` → To see if there is a PV, if not create one → `pvcreate /dev/partition_name`.
- `vgextend vg_name free_physical_volume_name` → To extend the VG.
- `lvextend -r -L +<size> /dev/group_name/lv_name` → To extend the LV (if an LV is already mounted with a file system -r: to also extend the file system).
- `lvs` → To verify.

#### Creating an LV with a number of PE (extent) and its PE size:
- `vgdisplay` → To see the PE.
- `vgcreate -s <size_extent> unity name_of_group /dev/pv_name /dev/pv_name…` → To create a volume group with the size of PE `size_extent`.
- `lvcreate -l <number> -n name_of_lv name_of_group` → To create an LV according to the number of PE.  
  **Size of PE * number of PE = size of LV**.
- `lvs` → To verify: the size should be `<number> * <size_extent>`.  
**Note**: To remove an LV, it must be unmounted (`umount lv_name`), comment the line in `/etc/fstab`, and run `mount -a`.  
- `lvremove /dev/group_name/lv_name`  
**Note**: To remove a VG, use `vgremove group_name`.

## IX. Container Management

### Apache Container

Launch an `httpd` container in Podman from the image `registry.access.redhat.com/ubi9/httpd-24` that meets the following conditions:  
- The container is started as a rootless container by the user `webadmin`.  
- The container must be accessible on port 8081 of the host (container = 8080).  
- The container uses the name `web`.  
- The directory `/home/webadmin/html` on the host must be mapped to `/var/www/html` in the container.  
- Generate a systemd service for this container (using the path `~/.config/systemd/user`).  

**Commands:**
- `podman run -d --name <container_name> -p <host_port>:<container_port> -v <local_path>:<container_path>:Z <image_id>` → `-p` option for port mapping.
- `podman rm --force <container_id>`  
- `podman ps`  
- `podman rmi --force <image_id>`  
- `podman images` → To remove a container.

```bash
useradd webadmin
passwd webadmin
loginctl enable-linger webadmin
mkdir /home/webadmin/html
echo ‘hi’ > /home/webadmin/html/index.html
chown webadmin:webadmin /home/webadmin/html
chown webadmin:webadmin /home/webadmin/html/index.html
ssh webadmin@localhost
podman pull registry.access.redhat.com/ubi9/httpd-24
podman images
podman inspect <image_id> | grep -i expose → Verify the container port to be created: 8080 for this image
podman run -d --name web -p 8081:8080 -v /home/webadmin/html:/var/www/html:Z <image_id>
podman ps
mkdir -p ~/.config/systemd/user
cd ~/.config/systemd/user
podman generate systemd --name web --files --new
systemctl --user daemon-reload
systemctl --user enable --now container-web.service
systemctl --user status container-web.service
curl localhost:8081
podman exec -it web bash
curl localhost:8080
(root) → journalctl | grep container-web.service

### PDF Converter Container

The "pdf-converter" container is designed to run a Python script named `pdf_converter.py` to convert text files into PDF files. The environment is configured to run under Red Hat using `Podman` instead of Docker. A `Dockerfile` is provided, detailing the steps to build the Podman image. Once the image is built, the container can be run to perform text-to-PDF conversion.

**Commands:**
- `dnf install podman container-tools` → Install Podman and container tools.
- `useradd pod` → Create the user `pod`.
- `passwd pod` → Set a password for the `pod` user.
- `mkdir -p /data/input /data/output` → Create the `input` and `output` directories.
- `chown -R pod:pod /data/*` → Change ownership of the `/data` directory and all its contents to the `pod` user.
- `ls -ld /data` → List the directories to verify ownership.
- `chown pod:pod /data` → Change the owner of `/data` to `pod`.
- `chmod -R 777 /data/*` or `chmod -R 777 /data/input`  
  `chmod -R 777 /data/output` → Add all permissions to the directories.
- `echo "file" > /data/input/file.txt` → Create a sample `.txt` file in the `input` directory to simulate conversion.
- `chown pod:pod /data/input/file.txt` → Change ownership of the `.txt` file to `pod`.
- `loginctl enable-linger pod` → Enable lingering for the `pod` user.
- `ssh pod@localhost` → SSH into the `pod` user account.
- `wget https://raw.githubusercontent.com/sachinyadav3496/Text-To-PDF/master/pdf_converter.py`  
  `wget https://raw.githubusercontent.com/sachinyadav3496/Text-To-PDF/master/Dockerfile`  
  → Download the `pdf_converter.py` script and `Dockerfile` needed for building the container image.
- `ls` → List the files to confirm the downloaded `Dockerfile` and Python script.
- `podman build -t pdf .` → Build the Podman image from the `Dockerfile`.
- `podman images` → Verify the image has been built.
- `podman run -d --name pdfconverter -v /data/input:/data/input:Z -v /data/output:/data/output:Z <image_id>`  
  → Run the container, mapping the `/data/input` directory locally to `/data/input` in the container (for `.txt` files), and `/data/output` locally to `/data/output` in the container (for PDF output).
- `podman ps` → Verify the running container.
- `mkdir -p ~/.config/systemd/user` → Create the systemd directory for the user.
- `cd ~/.config/systemd/user` → Navigate to the systemd user directory.
- `podman generate systemd --name pdfconverter --files --new` → Generate a systemd service file for the `pdfconverter` container.
- `systemctl --user daemon-reload` → Reload the systemd configuration.
- `systemctl --user enable --now container-pdfconverter.service` → Enable and start the container service.
- `systemctl --user restart --now container-pdfconverter.service` → Restart the service if needed.
- `systemctl --user status container-pdfconverter.service` → Check the status of the service.
- `podman exec -it pdfconverter bash` → Enter the container's shell.
- `ls /data/output` → Verify that the `.txt` file has been converted to a `.pdf` in the `output` directory.
- `exit` → Exit the container.
- `(root) reboot` → Reboot the system if necessary.
- `journalctl | grep container-pdfconverter.service` → Check the service logs as root.
``` 
## X. BaseOs & AppStream repositories

- `vim /etc/yum.repos.d/BaseOs.repo`
```bash
[BaseOs]
name=BaseOs
baseurl=…/BaseOs
enabled=1
(gpgcheck=1 (s’il ya un url key) sinon gpgcheck=0
gpgkey=…(s’il vous donne un url key))
```
- `vim /etc/yum.repos.d/AppStream.repo`
``` bash
[AppStream]
name= AppStream
baseurl=…/AppStream
enabled=1
(gpgcheck=1 (s’il ya un url key) sinon gpgcheck=0
gpgkey=…(s’il vous donne un url key))
```

## XI. Networks
### nmtui
👋 In this section, we will explore how to modify some network settings.
- `hostnamectl hostname name.example.com` → change the hostname.
- (It can be changed graphically) `nmtui` >> set system hostname name.example.com
- `nmtui` → manage the network graphically.
  - `edit a connection` >> `edit` >> `manual` >> `show: edit address, gateway, dns.` >> `ok`
  - NB: don’t forget to enable and disable the interface after modification.
  - `active a connection` >> `deactivate` >> `activate` >> `ok`
- `nmcli con sh` → check the interface (green).
### target:
- `systemctl isolate multi-user.target` → change the target to multi-user.
- `systemctl isolate graphical.target` → change the target to graphical.
- `loadkeys fr` → change the keyboard layout to azerty.
- `systemctl set-default graphical.target` → change the target to graphical, persists after reboot.
- `systemctl set-default multi-user.target` → change the target to multi-user, persists after reboot.
- `systemctl get-default` → check the default target.
### profile:
- `tuned`: to change the profile.
- `dnf install tuned` → install tuned.
- `tuned-adm recommend` → see the recommended profile.
- `tuned-adm active` → see my active profile.
- `tuned-adm list` → see all profiles.
- `tuned-adm profile <profile>` → change the profile.
- `systemctl restart tuned` → restart the service.
- `tuned-adm active` → check the active profile.

## XII. Root Password Reset

- `init=/bin/sh` → after the "quiet" word: to open a prompt
- `mount -o remount rw /`
- `passwd root`
- `new password retype new password`
- `touch /.autorelabel`
- `/usr/sbin/reboot -f`
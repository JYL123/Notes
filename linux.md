## Users and Groups 
In any traditional operating system, there are users and groups. They exist solely for access and permissions. 

Each user has their own home directory where their user specific files get stored, this is usually located in /home/username, but can vary in different distributions. The system uses user ids (UID) to manage users, usernames are the friendly way to associate users with identification, but the system identifies users by their UID. The system also uses groups to manage permissions, groups are just sets of users with permission set by that group, they are identified by the system with their group ID (GID).

In Linux, you'll have users in addition to the normal humans that use the system. Sometimes these users are system daemons that continuously run processes to keep the system functioning. One of the most important users is root or superuser, root is the most powerful user on the system, root can access any file and start and terminate any process. For that reason, it can be dangerous to operate as root all the time, you could potentially remove system critical files. Luckily, if root access is needed and a user has root access, they can run a command as root instead with the sudo command. The sudo command (superuser do) is used to run a command with root access, we'll go more in depth on how a user receives root access in a later lesson.

#### Files for user management
* The `/etc/shadow` file is used to store information about user authentication.
* The system uses a user ID (UID) to identify a user. To find out what users are mapped to what ID, look at the `/etc/passwd` file.
* Another file that is used in user management is the `/etc/group` file. This file allows for different groups with different permissions.

## Permissions

#### SUID
When a file has the SUID (**s**) permission set, it allows the users who launched the program to get the file owner's permission **as well as execution permission**.
SUID can be set via: `sudo chmod u+s myfile` or ` sudo chmod 4755 myfile` the SUID is denoted by a 4 and pre-pended to the permission set. You may see the SUID denoted as a capital **S** this means that it still does the same thing, but it **does not have execute permissions**.

#### SGID
This bit allows a program to run as if it was a member of that group. The numerical representation for SGID is 2. SGID is set via: `sudo chmod 2555 myfile` or `sudo chmod g+s myfile`.

#### Process Permissions
`Effective user ID`: this UID is used to grant access rights to a process. When you launch a process, it runs with the same permissions as the user or group that ran it.
`Real user ID`: the ID of the user that launched the process. These are used to track down who the user who launched the process is.
`Saved user ID`: this allows a process to switch between the effective UID and real UID, vice versa

#### Sticky bit
This permission bit, "sticks a file/directory" this means that only the owner or the root user can delete or modify the file. This is very useful for shared directories. 
```
drwxrwxrwxt 6 root root 4096 Dec 15 11:45 /tmp
```
You'll see a special permission bit at the end here t, this means everyone can add files, write files, modify files in the /tmp directory, but only root can delete the /tmp directory.

The numerical representation for the sticky bit is 1. The sticky bit can be set via: `sudo chmod +t mydir` or `sudo chmod 1755 mydir`.

## Processes `ps`
Processes are the programs that are running on your machine. They are managed by the kernel and each process has an ID associated with it called the process ID (PID). This PID is assigned in the order that processes are created.
```
$ ps


PID        TTY     STAT   TIME          CMD

41230    pts/4    Ss        00:00:00     bash

51224    pts/4    R+        00:00:00     ps

```
* **PID**: Process ID
* **TTY**: Controlling terminal associated with the process (we'll go in detail about this later)
* **STAT**: Process status code
* **TIME**: Total CPU usage time
* **CMD**: Name of executable/command

```
$ ps aux
```
**a** displays all processes running, including the ones being ran by other users. 
**u** shows more details about the processes. 
**x** lists all processes that don't have a TTY associated with it, these programs will show a ? in the TTY field, they are most common in daemon processes that launch as part of the system startup.

```
$ top
```
`top` command gives you real time information about the processes running on your system instead of a snapshot. By default you'll get a refresh every 10 seconds. Top is an extremely useful tool to see what processes are taking up a lot of your resources.

#### Process Details
A process like we said before is a running program on the system, more precisely it's the system allocating memory, CPU, I/O to make the program run.The `kernel` is in charge of processes, when we run a program the kernel loads up the code of the program in memory, determines and allocates resources and then keeps tabs on each process, it knows:
* The status of the process
* The resources the process is using and receives
* The process owner
* Signal handling (more on that later)
* And basically everything else

All processes are trying to get a taste of that sweet resource pie, it's the kernel's job to make sure that processes get the right amount of resources depending on process demands. When a process ends, the resources it used are now freed up for other processes.

#### Process Creation
When a new process is created, an existing process basically clones itself using something called the `fork` system call. The `fork` system call creates a mostly **identical** child process, this child process takes on a new process ID (PID) and the original process becomes its parent process and has something called a `parent process ID PPID`. Afterwards, the child process can either continue to use the same program its parent was using before or more often use the `execve` system call to launch up a new program. This system call destroys the memory management that the kernel put into place for that process and sets up new ones for the new program.

So if every process has to have a parent and they are just forks of each other, there must be a mother of all processes right? When the system boots up, the kernels creates a process called `init`, it has a PID of 1. The init process can't be terminated unless the system shuts down. It runs with root privileges and runs many processes that keep the system running.

## Init
The main purpose of init is to start and stop essential processes on the system. There are 3 major implementation of init in Linux, System V, Upstart, and Systemd. 

A `daemon` is a backgroud process of a Linux or Uniix program. Almost all daemons have names that end with 'd'. For example, `httpd` daemon handles the Apache server. 
`sshd` daemon handles the SSH remote access connection. 

`/etc/init.d/functions` file contains functions to be used by most or all shell scripts stored in /etc/init.d directory. The scripts in /etc/init.d are used to start,
stop, or restart the Linux and Unix system daemons. 

* [Launch upon start](http://developernotes.com/archive/2011/04/06/169.aspx)


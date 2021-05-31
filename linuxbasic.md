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
* **a** displays all processes running, including the ones being ran by other users. 
* **u** shows more details about the processes. 
* **x** lists all processes that don't have a TTY associated with it, these programs will show a ? in the TTY field, they are most common in daemon processes that launch as part of the system startup.

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

#### Process Termination
A process can exit using the `_exit` system call, this will free up the resources that process was using for reallocation. So when a process is ready to terminate, it lets the kernel know why it's terminating with something called a `termination status`. The parent process has to acknowledge the termination of the child process by using the `wait` system call and what this does is it checks the termination status of the child process.

**Orphan Processes** 
When a parent process dies before a child process, the kernel knows that it's not going to get a wait call, so instead it makes these processes "orphans" and puts them under the care of `init` (remember mother of all processes). `Init` will eventually perform the wait system call for these orphans so they can die.

**Zombie Processes**
What happens when a child terminates and the parent process hasn't called wait yet? We still want to be able to see how a child process terminated, so even though the child process finished, the kernel turns the child process into a zombie process. The resources the child process used are still freed up for other processes, however there is still an entry in the process table for this zombie. Zombie processes also cannot be killed, since they are technically "dead", so you can't use signals to kill them. Eventually if the parent process calls the wait system call, the zombie will disappear, this is known as "reaping". If the parent doesn't perform a wait call, init will adopt the zombie and automatically perform wait and remove the zombie. It can be a bad thing to have too many zombie processes, since they take up space on the process table, if it fills up it will prevent other processes from running.

#### Signals
A signal is a notification to a process that something has happened.

They are software interrupts and they have lots of uses:
* A user can type one of the special terminal characters (Ctrl-C) or (Ctrl-Z) to kill, interrupt or suspend processes
* Hardware issues can occur and the kernel wants to notify the process
* Software issues can occur and the kernel wants to notify the process
* They are basically ways processes can communicate

#### kill
```
kill 12445
```
The 12445 is the PID of the process you want to kill. By default it sends a TERM signal. The SIGTERM signal is sent to a process to request its termination by allowing it to cleanly release its resources and saving its state.

Differences between SIGHUP, SIGINT, SIGTERM, SIGKILL, SIGSTOP?

These signals all sound reasonably similar, but they do have their differences.
* **SIGHUP** - Hangup, sent to a process when the controlling terminal is closed. For example, if you closed a terminal window that had a process running in it, you would get a SIGHUP signal. So basically you've been hung up on
* **SIGINT** - Is an interrupt signal, so you can use Ctrl-C and the system will try to gracefully kill the process
* **SIGTERM** - Kill the process, but allow it to do some cleanup first
* **SIGKILL** - Kill the process, kill it with fire, doesn't do any cleanup
* **SIGSTOP** - Stop/suspend a process

#### Niceness
Niceness means is that processes have a number to determine their priority for the CPU. A high number means the process is nice and has a lower priority for the CPU and a low or negative number means the process is not very nice and it wants to get as much of the CPU as possible.

Niceness ranges from -20 to 19.

#### /proc filesystem
Remember everything in Linux is a file, even processes. Process information is stored in a special filesystem known as the /proc filesystem. The /proc directory is how the kernel is views the system, so there is a lot more information here than what you would see in ps.

#### Job Control 
**Sending a job to the background**
Appending an ampersand (**&**) to the command will run it in the background so you can still use your shell.

**View all background jobs**
```
$ jobs
```
The + next to the job ID means that it is the most recent background job that started. The job with the - is the second most recent command.

**Sending a job to the background on existing job**

If you already ran a job and want to send it to the background, you don't have to terminate it and start over again. First suspend the job with `Ctrl-Z`, then run the `bg` command to send it to the background.
```
pete@icebox ~ $ sleep 1003

^Z

[4]+    Stopped     sleep 1003


pete@icebox ~ $ bg

[4]+    sleep 1003 &



pete@icebox ~ $ jobs



[1]    Running     sleep 1000 &

[2]    Running     sleep 1001 &

[3]-   Running     sleep 1002 &

[4]+   Running     sleep 1003 &

```

**Moving a job from the background to the foreground**
```
$ fg %1
```
To move a job out of the background just specify the job ID you want. If you run `fg` without any options, it will bring back the most recent background job (the job with the + sign next to it)

**Kill background jobs**
```
kill %1
```
Similar to moving jobs out of the background, you can use the same form to kill the processes by using their Job ID.

## File System


#### Filesystem Hierarchy
* /bin - Essential ready-to-run programs (binaries), includes the most basic commands such as ls and cp.
* /boot - Contains kernel boot loader files.
* /dev - Device files.
* /etc - Core system configuration directory, should hold only configuration files and not any binaries.
* /home - Personal directories for users, holds your documents, files, settings, etc.
* /lib - Holds library files that binaries can use.
* /proc - Information about currently running processes.
* /root - The root user's home directory.
* /mnt - Temporarily mounted filesystems.
* /usr - This is unfortunately named, most often it does not contain user files in the sense of a home folder. This is meant for user installed software and utilities, however that is not to say you can't add personal directories in there. Inside this directory are sub-directories for /usr/bin, /usr/local, etc.

#### Creating Filesystems
```
$ sudo mkfs -t ext4 /dev/sdb2
```
The `mkfs` (make filesystem) tool allows us to specify the type of filesystem we want and where we want it. You'll only want to create a filesystem on a newly partitioned disk or if you are repartitioning an old one. You'll most likely leave your filesystem in a corrupted state if you try to create one on top of an existing one.

#### Mount and Umount
Before you can view the contents of your filesystem, you will have to mount it. To do that I'll need the device location, the filesystem type and a mount point, the mount point is a directory on the system where the filesystem is going to be attached. So we basically want to mount our device to a mount point.

```
$ sudo mount -t ext4 /dev/sdb2 /mydrive
```
Now when we go to /mydrive we can see our filesystem contents, the -t specifies the type of filesystem, then we have the device location, then the mount point.

To unmount a device from a mount point:
```
$ sudo umount /mydrive 

or 

$ sudo umount /dev/sdb2
```

## Boot Process
The Linux boot process can be broken down in 4 simple stages:

**1. BIOS**

The BIOS (stands for "Basic Input/Output System") initializes the hardware and makes sure with a Power-on self test (POST) that all the hardware is good to go. The main job of the BIOS is to load up the bootloader.

**2. Bootloader**

The bootloader loads the kernel into memory and then starts the kernel with a set of kernel parameters. One of the most common bootloaders is GRUB, which is a universal Linux standard.

**3. Kernel**

When the kernel is loaded, it immediately initializes devices and memory. The main job of the kernel is to load up the init process.

#### Initrd vs Initramfs
The kernel manages our systems hardware, however not all drivers are available to the kernel during bootup. So we depend on a temporary root filesystem that contains just the essential modules that the kernel needs to get to the rest of the hardware.

In older versions of Linux, this job was given to the `initrd (initial ram disk)`. The kernel would mount the initrd, get the necessary bootup drivers, then when it was done loading everything it needed, it would replace the initrd with the actual root filesystem.

These days, we have something called the `initramfs`, this is a temporary root filesystem that is built into the kernel itself to load all the necessary drivers for the real root filesystem, so no more locating the initrd file.

#### Mounting the root filesystem
Now the kernel has all the modules it needs to create a root device and mount the root partition. Before you go any further though, the root partition is actually mounted in read-only mode first so that `fsck` can run safely and check for system integrity. Afterwards it remounts the root filesystem in read-write mode. Then the kernel locates the init program and executes it.

The system utility **fsck** is a tool for checking the consistency of a file system in Unix and Unix-like operating systems, such as Linux, macOS, and FreeBSD. 

**4. Init**

Remember the init process is the first process that gets started, init starts and stops essential service process on the system. There are **three major implementations of init** in Linux distributions. We will go over them briefly and then dive into them in another course.

#### System V init (sysv)

This is the traditional init system. It sequentially starts and stops processes, based on startup scripts. The state of the machine is denoted by runlevels, each runlevel starts or stops a machine in a different way.

#### Upstart

This is the init you'll find on older Ubuntu installations. Upstart uses the idea of jobs and events and works by starting jobs that performs certain actions in response to events.

#### Systemd

This is the new standard for init, it is goal oriented. Basically you have a goal that you want to achieve and systemd tries to satisfy the goal's dependencies to complete the goal.

## Kernel
The Linux operating system can be organized into three different levels of abstraction.

The most basic level is hardware, this includes our CPU, memory, hard disks, networking ports, etc. The physical layer that actually computes what our machine is doing.

The next level is the kernel, which **handles process and memory management, device communication, system calls, sets up our filesystem, etc**. The kernel's job is to talk to the hardware to make sure it does what we want our processes to do.

And the level that you are familiar with is the user space, the user space includes the shell, the programs that you run, the graphics, etc.


## Init
The main purpose of init is to start and stop essential processes on the system. There are 3 major implementation of init in Linux, System V, Upstart, and Systemd. 

A `daemon` is a backgroud process of a Linux or Uniix program. Almost all daemons have names that end with 'd'. For example, `httpd` daemon handles the Apache server. 
`sshd` daemon handles the SSH remote access connection. 

`/etc/init.d/functions` file contains functions to be used by most or all shell scripts stored in /etc/init.d directory. The scripts in /etc/init.d are used to start,
stop, or restart the Linux and Unix system daemons. 

* [Launch upon start](http://developernotes.com/archive/2011/04/06/169.aspx)

reference:
* https://linuxjourney.com/

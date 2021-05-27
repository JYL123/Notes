The main purpose of init is to start and stop essential processes on the system. There are 3 major implementation of init in Linux, System V, Upstart, and Systemd. 

A `daemon` is a backgroud process of a Linux or Uniix program. Almost all daemons have names that end with 'd'. For example, `httpd` daemon handles the Apache server. 
`sshd` daemon handles the SSH remote access connection. 

`/etc/init.d/functions` file contains functions to be used by most or all shell scripts stored in /etc/init.d directory. The scripts in /etc/init.d are used to start,
stop, or restart the Linux and Unix system daemons. 


# Users and Privileges

&#x20;Looking at the screenshot a **"-"** means its a file if we se a "d" it is a directory rwxr **R**ead **W**rite E**x**ecute

&#x20;When doing pentesting, we're looking for a folder we can drop files in a directory that has full permissions i.e the /tmp/ folder on Linux

**chmod** this command can be used to change permissions 777 = full read write chmod 777 hello.txt will change the permissions of hello.txt to full read/write

Add a new user command **adduser** adduser john cat /etc/passwd to find new users added, this file contains all the users /etc/shadow contains the passwords

switch users command **su** su john

sudoers file contains users with root access

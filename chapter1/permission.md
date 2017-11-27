# User, Group, SuperUser
In Linux, there are two types of users: system users and regular users. Traditionally, system users are used to run non-interactive or background processes on a system, while regular users used for logging in and running processes interactively.

注:unix系统本身是针对实验室里老贵的机器的，那么就像实验室里其他死贵的机器一样，一开始就是很多人一起用的，现在家用机这个功能基本没啥用，但是在公司里区分员工权限还是比较靠谱的。

all users information are contained in the (*/etc/passwd*) file. One can print the passwd file with the following command
```bash
cat /etc/passwd    #catenate reads data from files, and outputs their contents standard output
```

---
***Groups*** are collections of zero or more users. A user belongs to a default group, and can also be a member of any of the other groups on a server.

```bash
cat /etc/group    #catenate reads data from files, and outputs their contents standard output
```
Or simply using *groups* command
```sh
groups    #List a user’s group memberships.
groups JoJoGroup #list user under this JoJoGroup
```
---
***SuperUser***

**sudo** ("*SUperuser DO*") allows a user with proper permissions to execute a command as another user, such as the superuser.

**su** ("*Switch User*") Change the current user ID to that of the superuser, or another user.


Syntax:
su [options] [username]


## Viewing Ownership and Permissions

```bash
ls -l      #list segment using long listing option
```

### What is Mode?

#### **File Type**

Two Basic file types in linux: *Normal* and *Special*.

#### **Normal files** are just plain files that can contain data.
Identified by files with a hyphen **(-)**

#### **Special files** can be identified by files that have a non-hyphen character,

For example, a Directory, which is the most common kind of special file, is identified by the **d** character



#### **Permission Class**

- **r**, Read
- **w**, Write
- **x**, Execute  


One can use number to present the permission:

| Number       | Permission           | Ref  |
| ------------- |:-------------:| -----:|
| 0      | No permission | --- |
| 1     | Execute permission     |  --x |
| 2 |Write permission    |   -w- |
| 3     |Execute and write permission: 1 (execute) + 2 (write) = 3 | -wx |
| 4     | Read permission    |  r-- |
| 5 |Read and execute permission: 4 (read) + 1 (execute) = 5    |   r-x |
| 6     | Read and write permission: 4 (read) + 2 (write) = 6   |  rw- |
| 7 |All permissions: 4 (read) + 2 (write) + 1 (execute) = 7   |   rwx |

### How to change mode, ownership, group

**chmod** (CHange MODe) change the permissions of files or directories.
Syntax：
**chmod [OPTION]... MODE[,MODE]... FILE...**

```sh
chmod u=rwx,g=rx,o=r myfile 
```
Equivalent command using octal 八进制(然而只是因为有8个而已) permission
```sh
chmod 754 myfile
```

[Mode] has the following format:

[ugoa...][[+-=][perms...]...]

A combination of the letters u, g, o, and a controls which users' access to the file will be changed: the user who owns it (u), other users in the file's group (g), other users not in the file's group (o), or all users (a).

"+" adding permission, "-" remove permission, "=" add or remove mentioned permission

```sh
chmod u+rwx myfile         #user owns myfile add rwx mode to permission
chmod go-x                 #group and other user remove execute permission
chmod a=x                  #all user add execute permission to the file 
```



**chown** (CHange OWNer)  changes the owner and owning group of files.
**chgrp** (CHange GRouP)  Changes group ownership of a file or files.

```sh
chown Chain textfile.txt  #Set the owner of textfile.txt to user Chain.
chown -R Chain /files/work  # Recursively grant ownership of the directory /files/work, and all files and subdirectories, to user Chain.
chgrp JoJoGroup textfile.txt # Change the owning group of the textfile to the group named JoJoGroup.
```

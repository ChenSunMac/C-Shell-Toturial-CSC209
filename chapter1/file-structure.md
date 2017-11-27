## Single Dierctory Hierarchy
The kernel maintains a **single hierarchical directory structure** to organize all files in the system. (This contrasts with operating systems such as *Microsoft Windows*, where each disk device has its own directory hierarchy.)

Every directory contains at least two entries: 

*. (dot)*, which is a link to the directory itself, and 

*.. (dot-dot)*, which is a link to its parent directory, for the root directory, it links to itself.

Each process has a ***current working directory (cwd)***. This is the process’s “current location” within the single directory hierarchy, and it is from this directory that relative pathnames are interpreted for the process.


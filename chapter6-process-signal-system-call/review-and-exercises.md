## True or False
**1.** If a process tries to read from an open pipe before there is any data in the Pipe, it could get an error. (2017 APRIL)
    
    + ***ANSWER***: read will be blocked until at least one byte has been written to the pipe. 




**2.** Open file descriptors are inherited across a fork call but not across an exec call.

    + ***ANSWER***: all file descriptors opened by a program that calls exec() remain open across the exec() and are available for use by the new program. If we want to close certain unused file descriptors, the exec call use *close-on-exec* flag


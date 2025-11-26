TryHackMe Compiled Walkthrough

Begin by downloading the provided executable. 

Running the command:

```bash

file <executable>.Compiled 

```

Produces the output:

```bash

<executable>.Compiled: ELF 64-bit LSB pie executable x86-64, version 1 SYSV, dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=06dcfaf13fb76a4b556852c5fbf9725ac21054fd, for GNU/Linux 3.2.0, not stripped

```

ELF executable (Executable and Linkable Format) is the standard binary format for Linux and is built on a 64-bit architecture for Intel/AMD.

Most importantly, it is not stripped. This means that the binary still contains: symbol names, function names, and debugging info. 

Before we boot this into Ghidra, let's quickly run the command:

```bash

strings <executable>.Compiled

```
Which gives the output:

```bash

/lib64/ld-linux-x86-64.so.2
jKUhR
__cxa_finalize
__libc_start_main
strcmp
stdout
__soc99_scanf
fwrite
printf
libc.so.6
GLIBC_2.7
GLIBC_2.2.5
GLIBC_2.34
_itm_deregisterTMCloneTable
__gmon_start__
_ITM_regiserTMCloneTable
PTE1
u+UH
StringsIH
sForNoobH
Password:
DoYouEven%sCTF
__dso_handle
_init
Correct!
Try again!
;*3$"
GCC: (Debian 11.3.0-5) 11.3.0
Scrt1.o
__abi_tag

```

Off the bat, what stands out is the line:

```bash

DoYouEven%sCTF

```

It also looks like the program output's 'Correct' if the password is correctly entered and 'Try again!' if incorrect.

Let's run the exectuable:

<img width="605" height="78" alt="3  trying password" src="https://github.com/user-attachments/assets/db668926-a80b-4cf4-853b-e379f4ac39ac" />

Trying the provided line earlier yields no results, as expected. 

This is most likely going to be our flag, or at least a snippet of it. 

Let's boot the exectuable up into Ghidra for analysis.

Let's navigate to the main logic of the code. 

<img width="556" height="375" alt="4  function in ghidra" src="https://github.com/user-attachments/assets/e7735362-3b0e-4c5f-9335-f211b573d9c4" />

Based on the logic above, it looks like if we replace '%sCTF' with '_nit' it should allow us in. 

<img width="582" height="82" alt="5 doyoueveninit" src="https://github.com/user-attachments/assets/40caf214-a04c-4035-bc2d-34e32a749ef6" />

The password is correct, and that is also our flag. 

Congratulations on completing the room!

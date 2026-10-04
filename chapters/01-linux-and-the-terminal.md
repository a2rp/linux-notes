# 1. Linux and the terminal

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Notes index](../README.md) | [Notes index](../README.md) | [Next: Filesystem and paths](./02-filesystem-and-paths.md) |

## What Linux means

Linux is the kernel at the center of an operating system. It manages hardware resources such as memory, processors, disks, and network devices. A Linux distribution combines that kernel with system tools, libraries, a package manager, and applications so the computer is ready to use.

Ubuntu, Debian, Fedora, and Arch Linux are distributions. They share many commands and concepts, but their package managers, default settings, and release policies differ. These notes explain shared ideas first and label distribution-specific commands.

## Terminal, shell, and command

A terminal is the text interface where you type commands and see their output. A shell reads what you type, finds a program or built-in command, and starts the requested work. Bash is a widely used shell.

A command usually has this shape:

~~~text
command [options] [arguments]
~~~

The command names the program or action. Options change its behavior. Arguments tell it what to work on. For example, in <code>uname -s</code>, <code>uname</code> is the command and <code>-s</code> asks it to print the kernel name.

## Run your first commands

Open a Linux terminal, or use a Linux virtual machine or Windows Subsystem for Linux. Try these read-only commands:

~~~sh
pwd
whoami
uname -srm
date
~~~

<code>pwd</code> prints the current directory. <code>whoami</code> prints the current account name. <code>uname -srm</code> prints the kernel name, release, and machine type. <code>date</code> prints the system date and time.

A command writes normal results to standard output. Error details often go to standard error. Both are text streams that can be saved or connected to other commands later.

## Read command help

Many commands provide a short help screen:

~~~sh
uname --help
~~~

Manual pages explain a command in more detail. Open one with:

~~~sh
man uname
~~~

Press <code>q</code> to leave a manual page. If <code>man</code> is unavailable, use a command's <code>--help</code> option or open its official documentation. Some commands, such as <code>cd</code>, are built into the shell and are documented in the Bash manual.

## Understand exit status

Every command returns an exit status when it finishes. Zero usually means success. A non-zero value indicates that something went wrong or that a condition was not met.

Read the last command's status with:

~~~sh
true
printf 'status: %s\n' "$?"
false
printf 'status: %s\n' "$?"
~~~

The first status is <code>0</code>; the second is non-zero. Check the status immediately because the next command replaces it.

## Practice safely

Begin with commands that inspect information. Before running a command that changes files or system settings, read its help, check the target path, and understand whether it needs elevated privileges. Use <code>sudo</code> only when an administrative task requires it, and do not paste commands you do not understand into a terminal.

To leave a shell session, type <code>exit</code>. Closing the terminal window also ends that terminal session.

## Practice questions

1. What part of the operating system is the Linux kernel responsible for?
2. How is a Linux distribution different from the kernel alone?
3. What does a shell do?
4. What information does <code>pwd</code> show?
5. What is the role of an option in a command?
6. What does an exit status of zero usually mean?
7. How can you get help for a command?
8. Why should you inspect a command before running it with elevated privileges?

## References

- [Welcome to the terminal](https://ubuntu.com/server/docs/tutorial/welcome-to-the-terminal/)
- [Linux manual pages](https://man7.org/linux/man-pages/)
- [GNU Bash Reference Manual](https://www.gnu.org/software/bash/manual/)
- [Linux kernel documentation](https://docs.kernel.org/)
# 7. Processes, jobs, and signals

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Users, groups, and sudo](./06-users-groups-and-sudo.md) | [Notes index](../README.md) | [Next: Packages and software](./08-packages-and-software.md) |

## What a process is

A running program is a process. The kernel assigns each process a process ID, or PID. A process also has a parent process ID, user identity, memory, open files, and a state. Child processes usually begin from another process.

List processes with <code>ps</code>:

~~~sh
ps
ps -ef
ps -eo pid,ppid,user,stat,comm
~~~

<code>ps -ef</code> shows a broad process list. The selected-column form makes the PID, parent PID, owner, state, and command easy to compare. Process states can include running, sleeping, stopped, or waiting to be collected after exit.

Use <code>top</code> to view a changing summary of processes and resource use. Press <code>q</code> to leave it.

## Find and stop a process

<code>pgrep</code> searches for processes by name. Add <code>-a</code> to show their command lines:

~~~sh
pgrep -a ssh
~~~

A process can receive a signal. <code>SIGTERM</code> asks it to stop and gives it a chance to clean up. Test on a process you started yourself:

~~~sh
sleep 300 &
process_id=$!
printf 'Started process: %s\n' "$process_id"
ps -p "$process_id" -o pid,stat,cmd
kill -TERM "$process_id"
~~~

The shell variable <code>$!</code> contains the PID of the most recently started background process. <code>kill</code> sends a signal. Despite its name, the default signal is normally a polite termination request.

<code>SIGKILL</code> stops a process immediately and cannot be handled by that process. Use it only if a process does not stop after a reasonable wait and you have verified the PID. Never copy a PID from an old listing without checking it again.

## Control jobs in a shell

A job is a command managed by the current interactive shell. Start a long-running command in the background by placing <code>&amp;</code> at the end:

~~~sh
sleep 300 &
jobs -l
~~~

In an interactive shell, press <code>Ctrl+Z</code> to suspend the foreground job. Use <code>bg</code> to continue it in the background, <code>fg</code> to bring it to the foreground, and <code>jobs</code> to list jobs in that shell.

Shell jobs belong to that shell session. Closing the terminal can send a hangup signal to jobs. For services that must keep running, configure a service manager rather than relying on a terminal job.

## Signals in practice

Signals are notifications delivered to a process. Common signals include:

| Signal | Common purpose |
| --- | --- |
| <code>SIGINT</code> | Interrupt from the terminal, commonly sent by <code>Ctrl+C</code> |
| <code>SIGTERM</code> | Request that a process exit cleanly |
| <code>SIGHUP</code> | Hangup notification, sometimes used by a program to reload configuration |
| <code>SIGKILL</code> | Force immediate termination |

The response depends on the program. For example, a service may treat <code>SIGHUP</code> as a request to reload, while another program may exit. Check the program's documentation before sending a signal.

## Practice questions

1. What does PID stand for?
2. Which <code>ps</code> form displays processes from all users?
3. What does <code>pgrep -a</code> include in its output?
4. What is the normal purpose of <code>SIGTERM</code>?
5. Why should <code>SIGKILL</code> be a last resort?
6. Which shell variable stores the last background process ID?
7. What does <code>Ctrl+Z</code> do to a foreground job?
8. Why should a long-running service be managed by a service manager?

## References

- [Linux manual page for ps](https://man7.org/linux/man-pages/man1/ps.1.html)
- [Linux manual page for kill](https://man7.org/linux/man-pages/man1/kill.1.html)
- [Linux manual page for proc](https://man7.org/linux/man-pages/man5/proc.5.html)
- [Linux signals documentation](https://man7.org/linux/man-pages/man7/signal.7.html)
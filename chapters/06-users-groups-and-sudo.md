# 6. Users, groups, and sudo

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Permissions, ownership, and ACLs](./05-permissions-ownership-and-acls.md) | [Notes index](../README.md) | [Next: Processes, jobs, and signals](./07-processes-jobs-and-signals.md) |

## User and group identity

Linux assigns each account a numeric user ID, called a UID. It assigns each group a numeric group ID, called a GID. Names make these IDs easier to read, while the IDs are what the kernel uses for permission checks.

Check your own identity and group membership with:

~~~sh
id
id ashish
groups
~~~

A user has one primary group and can belong to additional supplementary groups. File permissions use the owner and group recorded on the file. Group membership can therefore grant access to shared files and directories.

## Look up accounts and groups

The <code>getent</code> command queries the system's configured account databases:

~~~sh
getent passwd ashish
getent group developers
~~~

A passwd entry contains fields such as account name, UID, GID, home directory, and login shell. Password hashes are stored separately and are not printed by this command. Do not expose or copy password database contents.

Use <code>who</code> or <code>w</code> to see logged-in sessions:

~~~sh
who
w
~~~

The output can include usernames and session details, so treat it as system information.

## Administrator access with sudo

The root account has UID 0 and can make system-wide changes. The <code>sudo</code> command lets an approved user run a specific command with elevated privileges:

~~~sh
sudo systemctl status ssh
sudo -l
~~~

The first example checks a service status. The second lists commands the current account is allowed to run with <code>sudo</code>. An account may not have sudo permission, and service names differ by distribution.

Before adding <code>sudo</code>, ask whether an unprivileged command is enough. Run one elevated command at a time, check the target, and read the result. Do not run an entire shell as root unless a task truly requires it.

## Account administration

Account creation and group changes are administrative operations. On a system you administer, common commands include:

~~~sh
sudo adduser sam
sudo usermod -aG developers sam
sudo passwd sam
~~~

The command names and options can differ between distributions. The <code>-a</code> option in <code>usermod -aG</code> appends the supplementary group. Leaving out <code>-a</code> can replace the user's existing supplementary group list.

After changing group membership, the user may need to sign out and back in before a new session sees the change. Verify the result with <code>id sam</code>.

## Use the least access needed

Give each account only the access required for its work. Use groups for shared access instead of making files writable by everyone. For a one-off system task, prefer a single <code>sudo command</code> rather than changing ownership or permissions broadly.

## Practice questions

1. What does a UID identify?
2. What is the difference between a primary group and a supplementary group?
3. Which command displays your current user and group IDs?
4. What does UID 0 represent?
5. What does <code>sudo -l</code> show?
6. Why should elevated access be limited to the command that needs it?
7. What does the <code>-a</code> option preserve in <code>usermod -aG</code>?
8. Why might a user need to start a new session after a group change?

## References

- [Ubuntu user management documentation](https://ubuntu.com/server/docs/how-to/security/user-management/)
- [Linux manual page for sudo](https://man7.org/linux/man-pages/man8/sudo.8.html)
- [Linux manual page for id](https://man7.org/linux/man-pages/man1/id.1.html)
- [Linux manual page for usermod](https://man7.org/linux/man-pages/man8/usermod.8.html)
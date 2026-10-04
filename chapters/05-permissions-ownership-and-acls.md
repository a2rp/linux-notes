# 5. Permissions, ownership, and ACLs

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Reading, searching, and editing text](./04-reading-searching-and-editing-text.md) | [Notes index](../README.md) | [Next: Users, groups, and sudo](./06-users-groups-and-sudo.md) |

## Read a permission listing

Run <code>ls -l</code> to see file type, permission bits, owner, group, size, and modification time:

~~~sh
ls -l notes.txt
~~~

A mode such as <code>-rw-r-----</code> has a file-type character followed by three permission groups: owner, group, and everyone else. The letters mean read, write, and execute. A dash means that permission is absent.

For a regular file, read lets a user view contents, write lets them change contents, and execute lets them run it as a program. For a directory, read lists names, write changes directory entries, and execute allows traversal through the directory. Directory access therefore often needs both read and execute.

## Change permissions symbolically

Use <code>chmod</code> to change permissions. Symbolic mode names a class and the permission to add or remove:

~~~sh
chmod u+x script.sh
chmod g-w shared.txt
chmod o-r private.txt
~~~

The classes are <code>u</code> for owner, <code>g</code> for group, <code>o</code> for others, and <code>a</code> for all. The operators <code>+</code>, <code>-</code>, and <code>=</code> add, remove, or set permissions.

## Numeric permissions

Each permission has a value: read is 4, write is 2, and execute is 1. Add the values for each class to form a digit.

| Digit | Permissions |
| --- | --- |
| 7 | read, write, execute |
| 6 | read, write |
| 5 | read, execute |
| 4 | read only |
| 0 | no permissions |

The three digits represent owner, group, and others in that order:

~~~sh
chmod 640 private.txt
chmod 750 deploy.sh
~~~

Mode <code>640</code> gives the owner read and write, the group read, and others no access. Mode <code>750</code> also lets the owner run the script and lets group members read and run it.

Avoid assigning <code>777</code> as a quick fix. It gives every local user write access, which can expose data or allow files to be replaced.

## Change ownership

Use <code>chown</code> to change a file's owner. A colon can separate the owner and group:

~~~sh
sudo chown ashish:developers shared.txt
sudo chgrp developers shared.txt
~~~

Changing ownership usually requires administrator permission. Use the real account and group names on the system. On some systems, a user may change a file's group to a group they belong to.

## Default permissions and umask

New files and directories receive permissions based on a requested mode and the shell's umask. A common requested mode is 666 for files and 777 for directories. The umask removes permission bits from that starting mode.

~~~sh
umask
umask 027
touch private.txt
mkdir private-dir
ls -ld private.txt private-dir
~~~

With a umask of 027, common results are mode 640 for files and 750 for directories. Applications can request different modes. A umask setting affects the current shell and child processes; shell startup configuration determines whether it persists for a user session.

## Access control lists

Traditional mode bits assign access to one owner, one group, and others. An access control list can grant additional permissions to specific users or groups. Where ACL tools and filesystem support are available, inspect an ACL before changing it:

~~~sh
getfacl shared.txt
setfacl -m u:alex:r-- shared.txt
getfacl shared.txt
~~~

The example grants user <code>alex</code> read access. The named user still cannot exceed the effective permissions shown by the ACL mask. ACL syntax and package availability can vary by distribution.

## Practice questions

1. What three classes do the ordinary permission bits describe?
2. What does execute permission allow on a directory?
3. What is the numeric value for write permission?
4. What access does mode 640 give to the group?
5. Why is mode 777 risky for a private file?
6. What does a umask remove?
7. Which command changes a file's owner?
8. When is an ACL useful?

## References

- [Linux manual page for chmod](https://man7.org/linux/man-pages/man1/chmod.1.html)
- [Linux manual page for umask](https://man7.org/linux/man-pages/man2/umask.2.html)
- [Ubuntu user management documentation](https://ubuntu.com/server/docs/how-to/security/user-management/)
- [Linux manual page for getfacl](https://man7.org/linux/man-pages/man1/getfacl.1.html)
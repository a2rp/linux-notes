# 16. Boot, scheduling, and backups

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Security and troubleshooting](./15-security-and-troubleshooting.md) | [Notes index](../README.md) | [Next: All code samples](./98-all-code-samples.md) |

## A simple view of the boot process

After firmware initializes the machine, a bootloader loads the Linux kernel. The kernel detects hardware and starts the first user-space process. On a system that uses systemd, systemd then starts units such as services and mounts.

Inspect the current boot and default target:

~~~sh
systemd-analyze time
systemctl get-default
systemctl list-units --type=target
journalctl -b
~~~

<code>journalctl -b</code> shows messages from the current boot. To inspect an earlier boot, first list available boots with <code>journalctl --list-boots</code>, then select its index with the <code>-b</code> option.

## Schedule recurring work

A scheduled task runs at a chosen time without requiring an interactive terminal. Cron is common on many systems. Edit the current user's schedule with <code>crontab -e</code> and inspect it with <code>crontab -l</code>.

A cron entry has five time fields followed by a command:

~~~text
minute hour day-of-month month day-of-week command
~~~

For example, this entry runs a backup script every day at 2:15 in the morning:

~~~cron
15 2 * * * /home/ashish/bin/backup.sh
~~~

Use the actual absolute path to the script and any files it needs. Cron may provide a smaller environment than an interactive shell, so set required paths inside the script and direct output to a log or a mail destination supported by the system.

On a systemd-based machine, inspect available timers with:

~~~sh
systemctl list-timers --all
~~~

Use a systemd timer when a task should be managed alongside systemd units or when calendar and boot-time behavior need more control. Follow the distribution's service configuration practices.

## Create and inspect a backup archive

A compressed tar archive can store a directory tree in one file:

~~~sh
tar -czf "$HOME/linux-practice-backup.tar.gz" -C "$HOME" linux-practice
tar -tzf "$HOME/linux-practice-backup.tar.gz" | head
~~~

The first command creates an archive. The second lists its contents without extracting them. Check that expected files are present before relying on the backup.

Test restoration into a separate directory:

~~~sh
mkdir -p "$HOME/restore-test"
tar -xzf "$HOME/linux-practice-backup.tar.gz" -C "$HOME/restore-test"
find "$HOME/restore-test" -maxdepth 3 -type f -print
~~~

A backup is useful only if it can be restored. Keep a copy on separate storage or another system. A common planning rule is to keep multiple copies on different media and at least one copy in a separate location.

## Copy with rsync

<code>rsync</code> can synchronize directories. Use its dry-run option to preview changes:

~~~sh
rsync -a --dry-run "$HOME/linux-practice/" "$HOME/backup/linux-practice/"
~~~

After checking the source, destination, and preview, remove <code>--dry-run</code> to perform the copy. The <code>--delete</code> option can remove destination files that are missing from the source. Use it only when that exact mirror behavior is intended and the dry-run output is correct.

## Practice questions

1. Which component starts user-space services after the kernel?
2. What does <code>journalctl -b</code> show?
3. What are the five time fields in a cron entry?
4. Why should scheduled scripts use absolute paths?
5. Which command lists systemd timers?
6. How can you list the contents of a tar archive without extracting it?
7. Why should a backup be restored to a test location?
8. What can <code>rsync --delete</code> remove?

## References

- [systemd documentation](https://systemd.io/)
- [Linux manual page for journalctl](https://man7.org/linux/man-pages/man1/journalctl.1.html)
- [Linux manual page for crontab](https://man7.org/linux/man-pages/man5/crontab.5.html)
- [GNU tar manual](https://www.gnu.org/software/tar/manual/)
- [rsync manual](https://download.samba.org/pub/rsync/rsync.1)
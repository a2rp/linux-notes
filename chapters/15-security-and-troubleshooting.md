# 15. Security and troubleshooting

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Services, systemd, and logs](./14-services-systemd-and-logs.md) | [Notes index](../README.md) | [Next: Boot, scheduling, and backups](./16-boot-scheduling-and-backups.md) |

## Start with a few safe checks

When a system behaves unexpectedly, collect information before changing settings. These commands inspect uptime, memory, storage, failed units, and recent error messages:

~~~sh
uptime
free -h
df -h
systemctl --failed
journalctl -p err..alert -b
~~~

Check the affected service separately with <code>systemctl status</code> and its journal messages. Record the exact error and the time it occurred. Change one thing at a time so the result is clear.

## Keep access limited

Use a regular account for everyday work and elevate only commands that need administrator access. Keep file permissions narrow, use groups for shared access, and avoid making private files readable or writable by every user.

Protect SSH private keys with a passphrase and restrictive permissions:

~~~sh
chmod 700 "$HOME/.ssh"
chmod 600 "$HOME/.ssh/id_ed25519"
~~~

Never share a private key, password, access token, or a full configuration file that may contain credentials. Review logs and command output before posting them publicly.

## Apply updates from trusted sources

Install software and system updates through configured package sources. Confirm that package signatures and repository configuration are handled by the distribution's package manager. Do not disable security checks to force an installation.

Review the planned package changes before accepting them. For production systems, schedule changes, keep backups, and understand the recovery path.

## Use a firewall carefully

A host firewall controls which network traffic the system accepts. Ubuntu commonly provides UFW as a simpler interface to the kernel's packet filtering system.

~~~sh
sudo ufw status verbose
sudo ufw allow OpenSSH
sudo ufw enable
~~~

Before enabling a firewall on a remote machine, confirm the SSH rule and keep another recovery path available. A firewall can block your own connection if configured incorrectly. A firewall also does not replace account security, software updates, or correct file permissions.

## Check configuration before restarting

Many services can validate a configuration before applying it. For an OpenSSH server, a syntax check can catch mistakes:

~~~sh
sudo sshd -t
~~~

Only restart a service after its configuration passes validation and you know the service name and recovery steps. The server may use <code>sshd</code> or another unit name.

Linux systems may use AppArmor, SELinux, or another mandatory access control system. These controls can restrict what a process may access even when ordinary file permissions appear to allow it. Check the distribution documentation and audit logs before changing their policy.

## A practical troubleshooting sequence

1. Reproduce the problem and note the exact command and error.
2. Check the system state with read-only commands.
3. Inspect the relevant service status and logs.
4. Confirm paths, ownership, permissions, disk space, and network settings.
5. Make one small change and record what changed.
6. Repeat the original check, then undo the change if it did not help.

This sequence keeps observations separate from guesses and makes it easier to find the cause.

## Practice questions

1. Why should you collect information before changing system settings?
2. Which command lists failed systemd units?
3. Why should SSH private keys have restrictive permissions?
4. What should you confirm before enabling a firewall remotely?
5. Does a firewall replace user authentication?
6. What does <code>sshd -t</code> check?
7. Why should only one configuration change be made at a time?
8. What can AppArmor or SELinux restrict?

## References

- [Ubuntu security documentation](https://ubuntu.com/server/docs/how-to/security/)
- [Ubuntu firewall documentation](https://ubuntu.com/server/docs/firewalls/)
- [Linux manual page for journalctl](https://man7.org/linux/man-pages/man1/journalctl.1.html)
- [OpenSSH manual pages](https://www.openssh.com/manual.html)
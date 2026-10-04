# 14. Services, systemd, and logs

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Storage, filesystems, and mounts](./13-storage-filesystems-and-mounts.md) | [Notes index](../README.md) | [Next: Security and troubleshooting](./15-security-and-troubleshooting.md) |

## What a service is

A service is a program managed in the background, such as an SSH server or web server. Many Linux distributions use systemd to start services, track their state, and collect their logs.

Inspect service state with:

~~~sh
systemctl status ssh
systemctl list-units --type=service --state=running
systemctl is-enabled ssh
~~~

A service name can differ between distributions. For example, the SSH server unit may be named <code>ssh</code> on one system and <code>sshd</code> on another.

## Start, stop, and enable

Starting a service affects the current boot. Enabling it configures it to start automatically during future boots. These are separate actions.

~~~sh
sudo systemctl start ssh
sudo systemctl stop ssh
sudo systemctl restart ssh
sudo systemctl enable ssh
sudo systemctl enable --now ssh
sudo systemctl disable ssh
~~~

<code>restart</code> stops and starts a service. If a service supports a configuration reload, <code>systemctl reload</code> may apply configuration without a full restart. Check the service documentation first. Do not restart a remote access service on a server unless you have a way to recover access.

## Read service logs

The system journal stores messages from services and the system:

~~~sh
journalctl -u ssh
journalctl -u ssh --since '1 hour ago'
journalctl -u ssh -f
journalctl -b -p warning
~~~

<code>-u</code> filters by unit, <code>-f</code> follows new messages, <code>-b</code> selects the current boot, and <code>-p</code> filters by priority. Press <code>q</code> to exit the pager.

Use service status and logs together. The status output often includes recent messages and a short reason when a service has failed.

## Understand a unit file

A unit file describes how systemd should manage a service. This simplified example shows common fields:

~~~ini
[Unit]
Description=Example application
After=network.target

[Service]
Type=simple
User=linuxapp
WorkingDirectory=/opt/linuxapp
ExecStart=/usr/bin/python3 /opt/linuxapp/app.py
Restart=on-failure

[Install]
WantedBy=multi-user.target
~~~

The user, paths, executable, and startup requirements must match the actual application. A service should run as a dedicated unprivileged account when it does not need administrator access.

After changing or adding a unit file, ask systemd to reread unit definitions:

~~~sh
sudo systemctl daemon-reload
sudo systemctl status example.service
~~~

<code>daemon-reload</code> rereads unit files. It does not reload an application's own configuration. Use the application's supported reload operation for that.

## Practice questions

1. What does systemd manage?
2. How does starting a service differ from enabling it?
3. What does <code>systemctl enable --now</code> do?
4. Which command filters journal messages by unit?
5. What does <code>journalctl -f</code> do?
6. What does <code>systemctl daemon-reload</code> reread?
7. Why should a server service use a dedicated account when possible?
8. Why can restarting SSH be risky on a remote server?

## References

- [systemd documentation](https://systemd.io/)
- [systemd manual pages](https://www.freedesktop.org/software/systemd/man/)
- [Linux manual page for systemctl](https://man7.org/linux/man-pages/man1/systemctl.1.html)
- [Linux manual page for journalctl](https://man7.org/linux/man-pages/man1/journalctl.1.html)
# 99. Complete questions and answers

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: All code samples](./98-all-code-samples.md) | [Notes index](../README.md) | End of notes |

This appendix gathers the review questions from each chapter and provides a direct answer for every one.

## Chapter 1: Linux and the terminal

Source: [Open chapter](./01-linux-and-the-terminal.md)

### Question 1

What part of the operating system is the Linux kernel responsible for?

**Answer:** The kernel manages hardware resources and provides core services to programs.

### Question 2

How is a Linux distribution different from the kernel alone?

**Answer:** A distribution packages the Linux kernel with user-space tools, libraries, a package manager, and applications.

### Question 3

What does a shell do?

**Answer:** A shell reads command input, expands it, finds commands, and starts the requested work.

### Question 4

What information does <code>pwd</code> show?

**Answer:** <code>pwd</code> prints the shell current working directory.

### Question 5

What is the role of an option in a command?

**Answer:** An option changes how a command behaves or which information it reports.

### Question 6

What does an exit status of zero usually mean?

**Answer:** Exit status zero conventionally means that the command completed successfully.

### Question 7

How can you get help for a command?

**Answer:** Read the command manual page with <code>man</code> or try its <code>--help</code> option.

### Question 8

Why should you inspect a command before running it with elevated privileges?

**Answer:** Elevated commands can change system settings or data, so inspect the target and understand the command first.

## Chapter 2: Filesystem and paths

Source: [Open chapter](./02-filesystem-and-paths.md)

### Question 1

What character marks the root directory?

**Answer:** The slash character, <code>/</code>, names the root directory.

### Question 2

How does an absolute path differ from a relative path?

**Answer:** An absolute path begins at root. A relative path begins at the current working directory.

### Question 3

What does <code>..</code> mean in a path?

**Answer:** <code>..</code> refers to the parent directory.

### Question 4

What does the <code>HOME</code> variable contain?

**Answer:** <code>HOME</code> contains the current user home directory path.

### Question 5

Why should a path with spaces be quoted?

**Answer:** Quotes keep whitespace and special characters inside one path argument.

### Question 6

Where is system-wide configuration commonly stored?

**Answer:** <code>/etc</code> commonly stores system-wide configuration.

### Question 7

Why can <code>/proc</code> contain information that is not stored as ordinary disk files?

**Answer:** <code>/proc</code> is a virtual filesystem that exposes information provided by the running kernel.

### Question 8

Does a hidden filename automatically have restricted access?

**Answer:** No. A leading dot only hides a name from ordinary directory listings. File permissions control access.

## Chapter 3: Files and directories

Source: [Open chapter](./03-files-and-directories.md)

### Question 1

What does <code>mkdir -p</code> do?

**Answer:** It creates missing parent directories and does not fail when the target directory already exists.

### Question 2

How does <code>touch</code> behave when a file already exists?

**Answer:** It creates a missing empty file. For an existing file, it updates the modification time.

### Question 3

Which command renames a file?

**Answer:** <code>mv</code> renames or moves a file.

### Question 4

How can you ask before a copy overwrites a destination?

**Answer:** <code>cp -i</code> asks before replacing an existing destination.

### Question 5

Why is <code>rm -r</code> a command to use carefully?

**Answer:** Recursive removal can delete many files and does not normally send them to a trash folder.

### Question 6

What does <code>--</code> mean in the removal example?

**Answer:** <code>--</code> marks the end of options, so a following name beginning with a dash is treated as a filename.

### Question 7

What does the asterisk match in a shell pattern?

**Answer:** The asterisk matches any sequence of characters in shell filename expansion.

### Question 8

Which command can search a directory tree for matching files?

**Answer:** <code>find</code> searches a directory tree using conditions such as name and file type.

## Chapter 4: Reading, searching, and editing text

Source: [Open chapter](./04-reading-searching-and-editing-text.md)

### Question 1

When is <code>less</code> more useful than <code>cat</code>?

**Answer:** <code>less</code> is useful for browsing a long file a screen at a time without printing the whole file into the terminal.

### Question 2

How can you follow new lines added to a log file?

**Answer:** <code>tail -f filename</code> follows lines appended to a file until interrupted.

### Question 3

What does <code>wc -l</code> count?

**Answer:** <code>wc -l</code> counts lines.

### Question 4

Which <code>grep</code> option ignores letter case?

**Answer:** <code>grep -i</code> matches without regard to letter case.

### Question 5

What does <code>grep -v</code> select?

**Answer:** <code>grep -v</code> selects lines that do not match the pattern.

### Question 6

Why is <code>sort</code> often used before <code>uniq</code>?

**Answer:** <code>uniq</code> only collapses adjacent duplicate lines, so sorting brings equal values together first.

### Question 7

How does <code>cut</code> know where one field ends?

**Answer:** <code>cut</code> uses the delimiter option to identify field boundaries.

### Question 8

Which Nano shortcut saves the current file?

**Answer:** In Nano, <code>Ctrl+O</code> writes or saves the current file.

## Chapter 5: Permissions, ownership, and ACLs

Source: [Open chapter](./05-permissions-ownership-and-acls.md)

### Question 1

What three classes do the ordinary permission bits describe?

**Answer:** The ordinary permission classes are the owner, the file group, and other users.

### Question 2

What does execute permission allow on a directory?

**Answer:** Execute permission on a directory allows traversal through that directory.

### Question 3

What is the numeric value for write permission?

**Answer:** Write permission has numeric value 2.

### Question 4

What access does mode 640 give to the group?

**Answer:** Mode 640 gives the group read access and no write or execute access.

### Question 5

Why is mode 777 risky for a private file?

**Answer:** Mode 777 allows every local user to read, change, and execute the file, which can expose or corrupt it.

### Question 6

What does a umask remove?

**Answer:** A umask removes selected permission bits from the mode requested when a file or directory is created.

### Question 7

Which command changes a file's owner?

**Answer:** <code>chown</code> changes the owner of a file.

### Question 8

When is an ACL useful?

**Answer:** An ACL is useful when access needs to be granted to an additional named user or group without changing the main owner and group.

## Chapter 6: Users, groups, and sudo

Source: [Open chapter](./06-users-groups-and-sudo.md)

### Question 1

What does a UID identify?

**Answer:** A UID is the numeric identity assigned to a user account.

### Question 2

What is the difference between a primary group and a supplementary group?

**Answer:** A primary group is the account default group; supplementary groups grant additional group membership and access.

### Question 3

Which command displays your current user and group IDs?

**Answer:** <code>id</code> displays the current account UID, primary GID, and group memberships.

### Question 4

What does UID 0 represent?

**Answer:** UID 0 is the root administrator account.

### Question 5

What does <code>sudo -l</code> show?

**Answer:** <code>sudo -l</code> lists the commands the current account is permitted to run through sudo.

### Question 6

Why should elevated access be limited to the command that needs it?

**Answer:** Limiting elevated access reduces the effect of mistakes and keeps routine work under a regular account.

### Question 7

What does the <code>-a</code> option preserve in <code>usermod -aG</code>?

**Answer:** <code>-a</code> appends the named group while preserving the existing supplementary group list.

### Question 8

Why might a user need to start a new session after a group change?

**Answer:** A new login session refreshes group membership information held by the current session.

## Chapter 7: Processes, jobs, and signals

Source: [Open chapter](./07-processes-jobs-and-signals.md)

### Question 1

What does PID stand for?

**Answer:** PID means process ID, the number assigned to a running process.

### Question 2

Which <code>ps</code> form displays processes from all users?

**Answer:** <code>ps -ef</code> lists processes across users in a full-format listing.

### Question 3

What does <code>pgrep -a</code> include in its output?

**Answer:** <code>pgrep -a</code> includes each matching process command line.

### Question 4

What is the normal purpose of <code>SIGTERM</code>?

**Answer:** <code>SIGTERM</code> requests that a process exit cleanly and gives it a chance to close resources.

### Question 5

Why should <code>SIGKILL</code> be a last resort?

**Answer:** <code>SIGKILL</code> cannot be caught or handled, so the process cannot clean up before it stops.

### Question 6

Which shell variable stores the last background process ID?

**Answer:** <code>$!</code> contains the PID of the most recently started background process in the shell.

### Question 7

What does <code>Ctrl+Z</code> do to a foreground job?

**Answer:** <code>Ctrl+Z</code> suspends the foreground job in an interactive shell.

### Question 8

Why should a long-running service be managed by a service manager?

**Answer:** A service manager tracks the service beyond a shell session and can start it during system boot.

## Chapter 8: Packages and software

Source: [Open chapter](./08-packages-and-software.md)

### Question 1

What work does a package manager handle?

**Answer:** A package manager installs, updates, and removes software while tracking packages and dependencies.

### Question 2

What does <code>apt update</code> refresh?

**Answer:** <code>apt update</code> refreshes the local index of available packages.

### Question 3

Does <code>apt update</code> upgrade installed software?

**Answer:** No. It refreshes package metadata. <code>apt upgrade</code> applies available package upgrades.

### Question 4

Which command searches for an APT package?

**Answer:** <code>apt search name</code> searches configured package sources.

### Question 5

Which package manager is commonly used on Fedora?

**Answer:** Fedora commonly uses DNF.

### Question 6

What does <code>pacman -Syu</code> do on Arch Linux?

**Answer:** <code>pacman -Syu</code> refreshes package databases and upgrades installed packages on Arch Linux.

### Question 7

Why should package managers from different distributions not be mixed?

**Answer:** Mixing package managers can create inconsistent files and dependencies because each distribution manages its own package set.

### Question 8

What should you check before running a downloaded script with administrator access?

**Answer:** Verify the script source, read what it will do, and understand the privileges it requests before executing it.

## Chapter 9: Bash shell fundamentals

Source: [Open chapter](./09-bash-shell-fundamentals.md)

### Question 1

Why is <code>cd</code> usually built into the shell?

**Answer:** <code>cd</code> must update the current shell directory, which a separate child process could not change.

### Question 2

What does <code>export</code> do to a variable?

**Answer:** <code>export</code> marks a shell variable so child processes receive it in their environment.

### Question 3

What is <code>PATH</code> used for?

**Answer:** <code>PATH</code> lists directories that the shell searches when resolving executable command names.

### Question 4

How do single quotes treat a variable name inside them?

**Answer:** Text inside single quotes is treated literally, so a variable name is not expanded.

### Question 5

Why should variable expansions usually be quoted?

**Answer:** Quoting prevents whitespace splitting and wildcard expansion from turning one value into unintended arguments.

### Question 6

What does the command substitution around <code>date +%F</code> return?

**Answer:** It captures the date command output, formatted as year-month-day.

### Question 7

How does a question mark behave in a Bash filename pattern?

**Answer:** A question mark in a Bash filename pattern matches one character.

### Question 8

Why should secrets not be typed directly as command arguments?

**Answer:** Secrets can be visible in shell history or process listings when typed as command arguments.

## Chapter 10: Bash scripts and control flow

Source: [Open chapter](./10-bash-scripts-and-control-flow.md)

### Question 1

What does the shebang line select?

**Answer:** The shebang names the interpreter that should run the script.

### Question 2

How can you run a script that is in the current directory?

**Answer:** Use a relative path beginning with <code>./</code>, such as <code>./hello.sh</code>.

### Question 3

Which parameter contains the first argument?

**Answer:** <code>$1</code> contains the first positional argument.

### Question 4

Why does a script send error messages to standard error?

**Answer:** Standard error separates diagnostic messages from normal command results and can be redirected independently.

### Question 5

When is <code>case</code> useful?

**Answer:** <code>case</code> is useful when one value must be compared against several possible patterns.

### Question 6

Why does the example enable <code>nullglob</code>?

**Answer:** <code>nullglob</code> makes an unmatched wildcard expand to no names instead of remaining a literal pattern.

### Question 7

What does <code>local</code> do inside a function?

**Answer:** <code>local</code> limits a variable to the current function.

### Question 8

What does <code>bash -n</code> check?

**Answer:** <code>bash -n</code> checks script syntax without executing its commands.

## Chapter 11: Pipes, redirection, and text processing

Source: [Open chapter](./11-pipes-redirection-and-text-processing.md)

### Question 1

What does file descriptor 2 represent?

**Answer:** File descriptor 2 is standard error, commonly used for diagnostic messages.

### Question 2

How does append redirection differ from replace redirection?

**Answer:** <code>&gt;&gt;</code> appends to a file; <code>&gt;</code> replaces its existing contents.

### Question 3

What does a pipe pass to the next command?

**Answer:** A pipe passes the first command standard output as the next command standard input.

### Question 4

Which Bash option makes a pipeline reflect failures in earlier commands?

**Answer:** <code>set -o pipefail</code> makes a Bash pipeline report failure when an earlier command fails.

### Question 5

Why is <code>sort</code> used before <code>uniq</code> when counting values?

**Answer:** Sorting makes equal values adjacent, which is required for <code>uniq</code> to collapse or count all repeats.

### Question 6

When is <code>tee</code> useful?

**Answer:** <code>tee</code> sends input to the terminal and saves a copy to a file at the same time.

### Question 7

Why are null-delimited filenames safer with <code>xargs</code>?

**Answer:** Null delimiters do not conflict with spaces or newlines that may occur inside filenames.

### Question 8

Why should errors not be hidden while diagnosing a search?

**Answer:** Errors can show that some paths could not be read, so hiding them can make a search look complete when it is not.

## Chapter 12: Networking and SSH

Source: [Open chapter](./12-networking-and-ssh.md)

### Question 1

Which command displays local IP addresses?

**Answer:** <code>ip address</code> displays local network interfaces and their addresses.

### Question 2

What does <code>ip route</code> show?

**Answer:** <code>ip route</code> shows routing table entries used to choose a path to a destination.

### Question 3

Why can a failed ping occur while a web service is available?

**Answer:** Ping uses ICMP, which can be blocked while TCP or HTTP traffic is allowed.

### Question 4

What does <code>ss -ltn</code> list?

**Answer:** <code>ss -ltn</code> lists listening TCP sockets using numeric ports.

### Question 5

What does it mean for a service to listen on loopback?

**Answer:** Loopback means the service accepts connections from the local machine itself, not from other machines.

### Question 6

Which command checks HTTP response headers?

**Answer:** <code>curl -I URL</code> requests response headers.

### Question 7

Which SSH key should remain private?

**Answer:** The private key must stay with its owner and be protected; the public key is installed on the remote account.

### Question 8

Why should a server host key be verified?

**Answer:** Checking the fingerprint confirms that the SSH server has the expected identity and helps detect an unexpected server.

## Chapter 13: Storage, filesystems, and mounts

Source: [Open chapter](./13-storage-filesystems-and-mounts.md)

### Question 1

What is a filesystem responsible for?

**Answer:** A filesystem organizes names, directories, and file data on a storage volume.

### Question 2

What does a mount point connect?

**Answer:** A mount point is a directory where a filesystem is attached to the main Linux directory tree.

### Question 3

Which command shows filesystem types for block devices?

**Answer:** <code>lsblk -f</code> displays block devices with filesystem details.

### Question 4

What does <code>df -hT</code> report?

**Answer:** <code>df -hT</code> reports mounted filesystem types and their used and available space.

### Question 5

How does <code>du</code> differ from <code>df</code>?

**Answer:** <code>df</code> reports filesystem capacity; <code>du</code> estimates space used by files beneath a directory.

### Question 6

What does the <code>-o ro</code> mount option request?

**Answer:** <code>-o ro</code> asks to mount the filesystem read-only.

### Question 7

Why are UUIDs useful in persistent mount configuration?

**Answer:** A UUID identifies a filesystem independently of a device letter that may change.

### Question 8

Why must a device be verified before formatting it?

**Answer:** Formatting initializes a filesystem and can erase or make existing data inaccessible.

## Chapter 14: Services, systemd, and logs

Source: [Open chapter](./14-services-systemd-and-logs.md)

### Question 1

What does systemd manage?

**Answer:** Systemd manages system units such as services, mounts, and timers on systems that use it.

### Question 2

How does starting a service differ from enabling it?

**Answer:** Starting a service runs it now; enabling a service configures automatic startup at later boots.

### Question 3

What does <code>systemctl enable --now</code> do?

**Answer:** <code>systemctl enable --now</code> enables a unit for startup and starts it immediately.

### Question 4

Which command filters journal messages by unit?

**Answer:** <code>journalctl -u unit</code> filters journal entries for that unit.

### Question 5

What does <code>journalctl -f</code> do?

**Answer:** <code>journalctl -f</code> follows new journal messages as they arrive.

### Question 6

What does <code>systemctl daemon-reload</code> reread?

**Answer:** <code>systemctl daemon-reload</code> rereads systemd unit definitions from disk.

### Question 7

Why should a server service use a dedicated account when possible?

**Answer:** A dedicated unprivileged account limits what an application can access if it is compromised or misconfigured.

### Question 8

Why can restarting SSH be risky on a remote server?

**Answer:** If SSH fails to restart or its configuration is wrong, the remote administrator can lose the active connection and be unable to reconnect.

## Chapter 15: Security and troubleshooting

Source: [Open chapter](./15-security-and-troubleshooting.md)

### Question 1

Why should you collect information before changing system settings?

**Answer:** Read-only checks establish facts about system state and help avoid adding changes before the cause is understood.

### Question 2

Which command lists failed systemd units?

**Answer:** <code>systemctl --failed</code> lists failed systemd units.

### Question 3

Why should SSH private keys have restrictive permissions?

**Answer:** Restrictive permissions reduce the chance that other local users can read or copy the private key.

### Question 4

What should you confirm before enabling a firewall remotely?

**Answer:** Confirm remote access is allowed through the firewall and keep a recovery route before enabling it.

### Question 5

Does a firewall replace user authentication?

**Answer:** No. A firewall filters network traffic but does not verify a user password or replace application access controls.

### Question 6

What does <code>sshd -t</code> check?

**Answer:** <code>sshd -t</code> checks the SSH server configuration syntax.

### Question 7

Why should only one configuration change be made at a time?

**Answer:** One change at a time makes it clear which change affected the result.

### Question 8

What can AppArmor or SELinux restrict?

**Answer:** AppArmor and SELinux can restrict which files, capabilities, or system resources a process may access.

## Chapter 16: Boot, scheduling, and backups

Source: [Open chapter](./16-boot-scheduling-and-backups.md)

### Question 1

Which component starts user-space services after the kernel?

**Answer:** On a system using systemd, systemd starts and manages user-space services after the kernel starts the first user-space process.

### Question 2

What does <code>journalctl -b</code> show?

**Answer:** <code>journalctl -b</code> displays journal messages from the current boot.

### Question 3

What are the five time fields in a cron entry?

**Answer:** The fields are minute, hour, day of month, month, and day of week.

### Question 4

Why should scheduled scripts use absolute paths?

**Answer:** Cron can start with a limited environment, so absolute paths make it more likely that the intended script and files are found.

### Question 5

Which command lists systemd timers?

**Answer:** <code>systemctl list-timers --all</code> lists systemd timers, including inactive ones.

### Question 6

How can you list the contents of a tar archive without extracting it?

**Answer:** <code>tar -tzf archive.tar.gz</code> lists archive members without extracting them.

### Question 7

Why should a backup be restored to a test location?

**Answer:** A test restore confirms the archive can be read and expected files are present without overwriting the original data.

### Question 8

What can <code>rsync --delete</code> remove?

**Answer:** <code>rsync --delete</code> can remove destination files that are absent from the source.

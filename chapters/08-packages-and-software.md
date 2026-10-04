# 8. Packages and software

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Processes, jobs, and signals](./07-processes-jobs-and-signals.md) | [Notes index](../README.md) | [Next: Bash shell fundamentals](./09-bash-shell-fundamentals.md) |

## What a package manager does

A package manager installs software from configured sources, checks dependencies, records installed files, and provides a way to update or remove packages. Use the package manager for your distribution when possible so software can receive updates through the system's normal process.

Package names and available versions differ between distributions. Ubuntu and Debian commonly use APT, Fedora uses DNF, and Arch Linux uses Pacman. These commands are examples for their respective systems.

## APT on Ubuntu and Debian

APT separates refreshing the local package index from upgrading installed packages:

~~~sh
sudo apt update
apt list --upgradable
sudo apt upgrade
~~~

<code>apt update</code> downloads current package metadata. It does not upgrade installed programs. Review the list of available upgrades, then run <code>apt upgrade</code> when the system is ready.

Search for a package and inspect its details before installation:

~~~sh
apt search curl
apt show curl
sudo apt install curl
curl --version
~~~

Remove a package with <code>apt remove</code>. Review what the package manager proposes before confirming:

~~~sh
sudo apt remove curl
~~~

Some packages leave configuration files behind. A purge removes package configuration too, so use it only when that is intended. Review the proposed changes before approving any package operation.

## DNF and Pacman equivalents

On Fedora, DNF provides the corresponding operations:

~~~sh
sudo dnf check-update
sudo dnf upgrade
dnf search curl
sudo dnf install curl
sudo dnf remove curl
~~~

On Arch Linux, Pacman uses different options:

~~~sh
sudo pacman -Syu
pacman -Ss curl
sudo pacman -S curl
sudo pacman -R curl
~~~

Follow the release and package guidance for the distribution you actually use. Do not mix package managers from different distributions on one installation.

## Find the installed program

The shell can show which executable it will run:

~~~sh
command -v curl
curl --version
~~~

A program may be installed outside the package manager, for example in a user directory or through a language-specific tool. Check its source and update process before using it. Avoid running remote scripts as an administrator unless you have reviewed the script and trust its source.

## Plan system updates

Before upgrading an important system, check available disk space, confirm backups for important data, and read the distribution's release notes when changing releases. Security updates matter, but the timing of a larger upgrade should fit the system's maintenance plan.

## Practice questions

1. What work does a package manager handle?
2. What does <code>apt update</code> refresh?
3. Does <code>apt update</code> upgrade installed software?
4. Which command searches for an APT package?
5. Which package manager is commonly used on Fedora?
6. What does <code>pacman -Syu</code> do on Arch Linux?
7. Why should package managers from different distributions not be mixed?
8. What should you check before running a downloaded script with administrator access?

## References

- [Ubuntu package management documentation](https://ubuntu.com/server/docs/package-management/)
- [Ubuntu software management guidance](https://ubuntu.com/server/docs/package-management/)
- [DNF documentation](https://dnf.readthedocs.io/)
- [Pacman documentation](https://wiki.archlinux.org/title/Pacman)
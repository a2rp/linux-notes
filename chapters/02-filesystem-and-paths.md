# 2. Filesystem and paths

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Linux and the terminal](./01-linux-and-the-terminal.md) | [Notes index](../README.md) | [Next: Files and directories](./03-files-and-directories.md) |

## One directory tree

Linux presents files and directories through one tree that begins at the root directory, written as <code>/</code>. Disks and other storage can be mounted at directories in this tree. This is different from systems that show each disk as a separate drive letter.

A path names a location in the tree. A slash separates directory names. Linux paths are case-sensitive, so <code>/home/ashish/Notes</code> and <code>/home/ashish/notes</code> can refer to different locations.

## Absolute and relative paths

An absolute path starts with <code>/</code> and describes a location from the root. A relative path starts from the shell's current working directory.

~~~sh
pwd
ls /etc
ls ..
ls ./Documents
~~~

If the current directory is <code>/home/ashish</code>, then <code>../var</code> means <code>/home/var</code>. The special path <code>.</code> means the current directory and <code>..</code> means its parent.

## Home and current directories

Every user normally has a home directory for personal files. The shell stores its path in the <code>HOME</code> environment variable. A tilde at the start of a path is commonly expanded to the current user's home directory.

~~~sh
printf 'Home: %s\n' "$HOME"
cd ~
pwd
cd -
pwd
~~~

<code>cd</code> changes the current directory. With no argument, it changes to the home directory. <code>cd -</code> returns to the previous directory. <code>pwd</code> prints where the shell is now.

## Common top-level directories

The Filesystem Hierarchy Standard describes common locations. Systems may add directories or organize some details differently.

| Path | Common purpose |
| --- | --- |
| <code>/home</code> | Personal directories for regular users |
| <code>/root</code> | Home directory for the root administrator |
| <code>/etc</code> | System-wide configuration |
| <code>/usr</code> | Most installed programs, libraries, and shared read-only data |
| <code>/var</code> | Data that changes while the system runs, such as logs and caches |
| <code>/tmp</code> | Temporary files |
| <code>/dev</code> | Device files used to access hardware and virtual devices |
| <code>/proc</code> | Process and kernel information exposed by a virtual filesystem |
| <code>/sys</code> | Device and kernel information exposed by a virtual filesystem |
| <code>/mnt</code> and <code>/media</code> | Common mount locations |

Do not assume every file in these directories is a regular file stored on a disk. For example, <code>/proc</code> and <code>/sys</code> expose information provided by the running kernel.

## Spaces and special characters

Quote a path that contains spaces so the shell passes it as one argument:

~~~sh
cd "$HOME/Project Files"
ls "$HOME/Project Files"
~~~

Without quotes, the shell splits the path at spaces. Double quotes still allow variables such as <code>HOME</code> to expand. Single quotes preserve text literally, but do not expand variables.

## Inspect a path

Use <code>ls -lah</code> to see names, hidden entries, permissions, owners, and sizes in a directory:

~~~sh
ls -lah "$HOME"
~~~

Names beginning with a dot are hidden from the usual <code>ls</code> listing. The <code>-a</code> option includes them. Hidden does not mean protected; permissions still control access.

The <code>realpath</code> command can display a normalized absolute path:

~~~sh
realpath .
realpath "$HOME/Project Files"
~~~

<code>realpath</code> is provided by GNU coreutils on many distributions. If it is unavailable, use <code>pwd</code> after changing to the directory.

## Practice questions

1. What character marks the root directory?
2. How does an absolute path differ from a relative path?
3. What does <code>..</code> mean in a path?
4. What does the <code>HOME</code> variable contain?
5. Why should a path with spaces be quoted?
6. Where is system-wide configuration commonly stored?
7. Why can <code>/proc</code> contain information that is not stored as ordinary disk files?
8. Does a hidden filename automatically have restricted access?

## References

- [Filesystem Hierarchy Standard](https://refspecs.linuxfoundation.org/FHS_3.0/fhs/index.html)
- [Ubuntu command line documentation](https://ubuntu.com/server/docs/)
- [GNU coreutils manual](https://www.gnu.org/software/coreutils/manual/)
- [Linux manual page for path_resolution](https://man7.org/linux/man-pages/man7/path_resolution.7.html)
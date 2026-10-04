# 3. Files and directories

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Filesystem and paths](./02-filesystem-and-paths.md) | [Notes index](../README.md) | [Next: Reading, searching, and editing text](./04-reading-searching-and-editing-text.md) |

## Create directories and files

Use <code>mkdir</code> to create a directory. The <code>-p</code> option also creates missing parent directories and does not report an error if the target already exists.

~~~sh
mkdir -p "$HOME/linux-practice/work"
cd "$HOME/linux-practice/work"
touch notes.txt
~~~

<code>touch</code> creates an empty file when it does not exist. If the file exists, it updates its modification time without changing its contents.

## Copy and move

<code>cp</code> copies a file. <code>mv</code> moves or renames it. Quote paths so spaces remain part of a single name.

~~~sh
printf 'Linux practice notes\n' > notes.txt
cp notes.txt notes-copy.txt
mv notes-copy.txt saved-notes.txt
ls -l
~~~

Copy a directory and its contents recursively with <code>cp -r</code>. For a local backup that should preserve common file attributes, GNU <code>cp -a</code> is often useful.

~~~sh
mkdir -p project/docs
printf 'Draft\n' > project/docs/readme.txt
cp -a project project-backup
~~~

Use <code>cp -i</code> or <code>mv -i</code> when you want a prompt before overwriting a destination:

~~~sh
cp -i notes.txt saved-notes.txt
mv -i saved-notes.txt notes.txt
~~~

## Remove files and directories

<code>rm</code> removes files. It does not normally move them to a trash folder, so check the path before confirming:

~~~sh
rm -i notes.txt
~~~

The <code>-i</code> option asks before each removal. Use <code>rmdir</code> to remove an empty directory. Removing a directory tree requires recursive removal, often written as <code>rm -r</code>. Treat recursive removal as destructive. Inspect the target with <code>pwd</code> and <code>ls</code> first, and avoid running it with an unexpanded or uncertain variable.

A leading dash in a filename can be mistaken for an option. Use <code>--</code> to mark the end of options:

~~~sh
rm -- -temporary-file
~~~

## Work with groups of names

The shell expands patterns before passing them to a command. The asterisk matches any sequence of characters, and the question mark matches one character.

~~~sh
ls *.txt
cp report-?.txt "$HOME/linux-practice/"
~~~

A pattern may match many files. Preview the matching names with <code>printf</code> or <code>ls</code> before using it with a command that changes or removes files.

Bash also supports brace expansion for a known set of names:

~~~sh
mkdir -p "$HOME/linux-practice"/{docs,images,logs}
~~~

Brace expansion is a Bash feature and may not work in every shell.

## Inspect files and directories

Use <code>file</code> to inspect a file's type, <code>stat</code> to inspect metadata, and <code>find</code> to search a directory tree.

~~~sh
file notes.txt
stat notes.txt
find "$HOME/linux-practice" -type f -name '*.txt' -print
~~~

GNU <code>find</code> evaluates tests from left to right. The example only prints matching paths. Add actions such as deletion only after understanding how the search expression matches.

## Practice questions

1. What does <code>mkdir -p</code> do?
2. How does <code>touch</code> behave when a file already exists?
3. Which command renames a file?
4. How can you ask before a copy overwrites a destination?
5. Why is <code>rm -r</code> a command to use carefully?
6. What does <code>--</code> mean in the removal example?
7. What does the asterisk match in a shell pattern?
8. Which command can search a directory tree for matching files?

## References

- [GNU coreutils manual](https://www.gnu.org/software/coreutils/manual/)
- [Linux manual page for find](https://man7.org/linux/man-pages/man1/find.1.html)
- [Linux manual page for file](https://man7.org/linux/man-pages/man1/file.1.html)
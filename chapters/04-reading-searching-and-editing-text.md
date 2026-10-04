# 4. Reading, searching, and editing text

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Files and directories](./03-files-and-directories.md) | [Notes index](../README.md) | [Next: Permissions, ownership, and ACLs](./05-permissions-ownership-and-acls.md) |

## Read a file

Use <code>cat</code> to print a short file. For a long file, <code>less</code> lets you move through the contents without loading the whole display at once.

~~~sh
cat notes.txt
less /etc/services
~~~

Inside <code>less</code>, press <code>Space</code> to move forward, <code>b</code> to move backward, and <code>q</code> to quit.

Use <code>head</code> and <code>tail</code> to inspect the beginning or end of a file:

~~~sh
head -n 10 notes.txt
tail -n 20 notes.txt
tail -f application.log
~~~

The <code>-f</code> option follows new lines as they are added. Press <code>Ctrl+C</code> to stop following the file.

## Count and search

<code>wc</code> counts lines, words, and bytes. Its options select one count:

~~~sh
wc notes.txt
wc -l notes.txt
wc -w notes.txt
~~~

Use <code>grep</code> to find lines containing a pattern:

~~~sh
grep -n 'error' application.log
grep -i 'warning' application.log
grep -v '^#' settings.conf
~~~

<code>-n</code> includes line numbers, <code>-i</code> ignores letter case, and <code>-v</code> selects lines that do not match. Quote patterns so the shell does not interpret special characters before <code>grep</code> receives them.

Search subdirectories recursively with <code>-r</code>. Restricting the search to a file pattern can keep the result focused:

~~~sh
grep -r --include='*.conf' 'timeout' ./config
~~~

## Inspect structured text

Standard utilities can select or reorder columns in simple text files. These examples create a small file, then inspect its contents:

~~~sh
cat > services.txt <<'EOF'
web active 8080
worker paused 0
cache active 6379
EOF

cut -d ' ' -f 1 services.txt
sort services.txt
sort services.txt | uniq
~~~

<code>cut</code> selects a field using a delimiter. <code>sort</code> orders lines. <code>uniq</code> removes adjacent duplicate lines, so data often needs sorting first when the goal is to count all repeated values.

These commands work best with predictable delimiters. For nested or quoted formats such as JSON, use a parser made for that format instead of assuming that every space or comma has the same meaning.

## Edit a text file

<code>nano</code> is a small terminal editor. Open a file with:

~~~sh
nano notes.txt
~~~

Nano shows its main shortcuts at the bottom of the screen. <code>Ctrl+O</code> saves, <code>Enter</code> confirms the filename, and <code>Ctrl+X</code> exits. Other editors, such as Vim, are also common. Check which editor is available before relying on it in a remote environment.

For repeatable changes, prefer a clear editor session or a small script. Commands such as <code>sed</code> can transform text, but an in-place edit changes the original file. Test a transformation on a copy or print its output before saving it.

## Practice questions

1. When is <code>less</code> more useful than <code>cat</code>?
2. How can you follow new lines added to a log file?
3. What does <code>wc -l</code> count?
4. Which <code>grep</code> option ignores letter case?
5. What does <code>grep -v</code> select?
6. Why is <code>sort</code> often used before <code>uniq</code>?
7. How does <code>cut</code> know where one field ends?
8. Which Nano shortcut saves the current file?

## References

- [GNU grep manual](https://www.gnu.org/software/grep/manual/)
- [GNU coreutils manual](https://www.gnu.org/software/coreutils/manual/)
- [GNU sed manual](https://www.gnu.org/software/sed/manual/)
- [Linux manual pages](https://man7.org/linux/man-pages/)
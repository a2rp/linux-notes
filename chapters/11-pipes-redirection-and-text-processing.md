# 11. Pipes, redirection, and text processing

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Bash scripts and control flow](./10-bash-scripts-and-control-flow.md) | [Notes index](../README.md) | [Next: Networking and SSH](./12-networking-and-ssh.md) |

## Three standard streams

A command normally reads from standard input and writes to standard output. Diagnostic messages are commonly written to standard error. Their file descriptor numbers are 0, 1, and 2.

Redirect output to a file. A single greater-than sign replaces the file; two greater-than signs append to it:

~~~sh
printf 'first line\n' > notes.txt
printf 'another line\n' >> notes.txt
cat notes.txt
~~~

Redirect standard error separately with <code>2&gt;</code>:

~~~sh
find "$HOME" -name '*.conf' -print 2> find-errors.txt
~~~

This keeps permission errors in a separate file. Do not discard errors when they might explain missing results.

Use <code>&lt;</code> to read input from a file:

~~~sh
wc -l < notes.txt
~~~

## Connect commands with a pipe

A pipe sends one command's standard output to the next command's standard input:

~~~sh
ps -ef | grep '[s]sh'
grep -i 'error' application.log | wc -l
~~~

Pipes allow small commands to work together. In the first example, <code>grep</code> narrows the process list. The bracket pattern avoids matching the grep command itself.

A pipeline normally returns the status of its last command. In Bash, <code>set -o pipefail</code> makes a pipeline fail if any command in it fails:

~~~bash
set -o pipefail
grep 'ERROR' application.log | sort | uniq -c
~~~

## Inspect and reshape text

Common text filters include:

| Command | Common use |
| --- | --- |
| <code>grep</code> | Select lines that match a pattern |
| <code>cut</code> | Select fields separated by a chosen character |
| <code>sort</code> | Sort lines |
| <code>uniq</code> | Collapse adjacent repeated lines |
| <code>tr</code> | Translate or remove characters |
| <code>awk</code> | Select fields and apply simple rules |

For example, count repeated status values in a space-separated file:

~~~sh
cut -d ' ' -f 2 services.txt | sort | uniq -c
~~~

The delimiter and field number must match the file's layout. For complex formats such as CSV with quoted commas or JSON, use a parser that understands that format.

## Save and view a pipeline

The <code>tee</code> command writes input to both the screen and a file:

~~~sh
grep -i 'warning' application.log | tee warnings.txt
~~~

By default, <code>tee</code> replaces its output file. Its append option adds to the existing file. Check which output file a pipeline writes before running it against important data.

## Use xargs carefully

<code>xargs</code> builds command arguments from its input. Filenames can contain spaces and newlines, so null-delimited paths are safer:

~~~sh
find "$HOME/linux-practice" -type f -name '*.tmp' -print0 |
    xargs -0 -r printf 'Matched: %s\n'
~~~

This example only prints matching names. If you use <code>xargs</code> to remove or change files, review the printed list first and understand exactly what the command will receive.

## Practice questions

1. What does file descriptor 2 represent?
2. How does append redirection differ from replace redirection?
3. What does a pipe pass to the next command?
4. Which Bash option makes a pipeline reflect failures in earlier commands?
5. Why is <code>sort</code> used before <code>uniq</code> when counting values?
6. When is <code>tee</code> useful?
7. Why are null-delimited filenames safer with <code>xargs</code>?
8. Why should errors not be hidden while diagnosing a search?

## References

- [GNU Bash Reference Manual: redirections](https://www.gnu.org/software/bash/manual/html_node/Redirections.html)
- [GNU Bash Reference Manual: pipelines](https://www.gnu.org/software/bash/manual/html_node/Pipelines.html)
- [GNU coreutils manual](https://www.gnu.org/software/coreutils/manual/)
- [GNU findutils manual](https://www.gnu.org/software/findutils/manual/)
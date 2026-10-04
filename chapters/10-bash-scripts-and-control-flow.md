# 10. Bash scripts and control flow

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Bash shell fundamentals](./09-bash-shell-fundamentals.md) | [Notes index](../README.md) | [Next: Pipes, redirection, and text processing](./11-pipes-redirection-and-text-processing.md) |

## Make a Bash script

A shell script is a text file containing commands. A shebang on the first line selects the interpreter:

~~~bash
#!/usr/bin/env bash
printf 'Hello from Bash\n'
~~~

Save it as <code>hello.sh</code> and run it with Bash:

~~~sh
bash hello.sh
~~~

To run a script by its path, give it execute permission:

~~~sh
chmod u+x hello.sh
./hello.sh
~~~

The current directory is not normally searched when you type a command name, so use <code>./</code> to run a script from the current directory.

## Arguments and exit codes

Arguments let a script work with different input each time. <code>$1</code> is the first argument, <code>$2</code> is the second, and <code>$#</code> is the number of arguments. Use <code>"$@"</code> when forwarding all arguments while preserving each one as a separate value.

This script requires a directory and returns a useful status when it is missing:

~~~bash
#!/usr/bin/env bash

if [[ $# -ne 1 ]]; then
    printf 'Usage: %s DIRECTORY\n' "$0" >&2
    exit 2
fi

directory=$1
if [[ ! -d $directory ]]; then
    printf 'Directory not found: %s\n' "$directory" >&2
    exit 1
fi

printf 'Reading files from %s\n' "$directory"
exit 0
~~~

Programs conventionally use status 0 for success and a non-zero value for an error or unmet condition. Send error details to standard error with <code>&gt;&amp;2</code>.

## Conditions and case choices

Bash conditions use <code>if</code> and test expressions. The double-bracket form supports string, file, and numeric checks:

~~~bash
if [[ -f "$1" ]]; then
    printf 'Regular file\n'
elif [[ -d "$1" ]]; then
    printf 'Directory\n'
else
    printf 'Path does not exist or has another type\n'
fi
~~~

Use <code>case</code> when one value has several expected patterns:

~~~bash
case "$1" in
    start) printf 'Starting\n' ;;
    stop) printf 'Stopping\n' ;;
    status) printf 'Checking status\n' ;;
    *) printf 'Choose start, stop, or status\n' >&2; exit 2 ;;
esac
~~~

## Loops and functions

A <code>for</code> loop processes a list. This example counts log files in a directory:

~~~bash
shopt -s nullglob
count=0
for log_file in "$directory"/*.log; do
    count=$((count + 1))
done
printf 'Log files: %d\n' "$count"
~~~

With <code>nullglob</code>, a pattern that matches no files expands to an empty list. Without it, the loop could receive the literal pattern as a filename.

A function groups commands that belong together:

~~~bash
print_file_type() {
    local path=$1
    if [[ -f $path ]]; then
        printf '%s: regular file\n' "$path"
    elif [[ -d $path ]]; then
        printf '%s: directory\n' "$path"
    else
        printf '%s: not found\n' "$path"
        return 1
    fi
}

print_file_type "$HOME"
~~~

Use <code>local</code> for variables that should stay inside a function. A function's return status is separate from text it prints.

## A complete small script

Save this as <code>count-logs.sh</code>. It validates its input and safely handles a directory with no matching files:

~~~sh
cat > count-logs.sh <<'SCRIPT'
#!/usr/bin/env bash
set -u

if [[ $# -ne 1 ]]; then
    printf 'Usage: %s DIRECTORY\n' "$0" >&2
    exit 2
fi

directory=$1
if [[ ! -d $directory ]]; then
    printf 'Directory not found: %s\n' "$directory" >&2
    exit 1
fi

shopt -s nullglob
count=0
for log_file in "$directory"/*.log; do
    count=$((count + 1))
done

printf 'Found %d log files in %s\n' "$count" "$directory"
SCRIPT

chmod u+x count-logs.sh
bash -n count-logs.sh
./count-logs.sh "$HOME"
~~~

<code>bash -n</code> checks Bash syntax without running the script. <code>bash -x</code> prints expanded commands as the script runs, which can help find a logic mistake. Review that output before sharing it because it may include sensitive values.

## Practice questions

1. What does the shebang line select?
2. How can you run a script that is in the current directory?
3. Which parameter contains the first argument?
4. Why does a script send error messages to standard error?
5. When is <code>case</code> useful?
6. Why does the example enable <code>nullglob</code>?
7. What does <code>local</code> do inside a function?
8. What does <code>bash -n</code> check?

## References

- [GNU Bash Reference Manual](https://www.gnu.org/software/bash/manual/)
- [Bash shell scripts](https://www.gnu.org/software/bash/manual/html_node/Shell-Scripts.html)
- [Bash conditional constructs](https://www.gnu.org/software/bash/manual/html_node/Conditional-Constructs.html)
- [Bash shell functions](https://www.gnu.org/software/bash/manual/html_node/Shell-Functions.html)
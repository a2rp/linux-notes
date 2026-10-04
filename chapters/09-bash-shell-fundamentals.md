# 9. Bash shell fundamentals

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Packages and software](./08-packages-and-software.md) | [Notes index](../README.md) | [Next: Bash scripts and control flow](./10-bash-scripts-and-control-flow.md) |

## How Bash reads a command

Bash reads a command line, expands variables and patterns, splits words where allowed, and then runs a command. Quoting controls which parts of this process happen. Many shell mistakes come from assuming that a line is passed to a program exactly as typed.

Find out how Bash interprets a name:

~~~sh
type cd
type printf
command -v bash
~~~

<code>cd</code> is normally a shell built-in because a separate program could not change the parent shell's working directory. <code>command -v</code> shows how a command name resolves in the current shell.

## Variables and environment

Assign a value with no spaces around the equals sign:

~~~sh
project_name='linux-practice'
printf '%s\n' "$project_name"
~~~

A shell variable belongs to the current shell. Child processes receive only variables exported into the environment:

~~~sh
export APP_MODE=development
printenv APP_MODE
~~~

Environment variables such as <code>HOME</code>, <code>USER</code>, <code>SHELL</code>, and <code>PATH</code> help programs find user settings, identify the account, and locate executables. <code>PATH</code> is a list of directories separated by colons.

Use a default when a variable may be empty or unset:

~~~sh
printf 'Editor: %s\n' "$EDITOR"
~~~

## Quote your values

Single quotes preserve their contents literally. Double quotes still allow variable and command substitutions but keep the expanded result as one argument.

~~~sh
name='Sam Lee'
printf 'Hello, %s\n' "$name"
printf '%s\n' '$HOME is literal text'
printf '%s\n' "$HOME"
~~~

Unquoted expansions can split on whitespace and expand wildcard characters. Quote variable expansions unless you intentionally want word splitting or pattern matching.

## Command substitution

Use the dollar-parentheses form to capture a command's output as part of another value:

~~~sh
today=$(date +%F)
printf 'Date: %s\n' "$today"
~~~

An older substitution form also exists, but nested commands are harder to read. Prefer the dollar-parentheses form.

## Patterns and expansion

The shell expands wildcard patterns before running most commands:

~~~sh
printf '%s\n' *.md
printf '%s\n' report-?.txt
~~~

An asterisk matches any sequence of characters. A question mark matches one character. If no file matches, Bash usually passes the original pattern through unchanged unless its options have been changed.

Brace expansion makes a known list of strings:

~~~sh
printf '%s\n' chapter-{01,02,03}.md
~~~

Brace expansion is performed by Bash and does not check whether those files exist.

## History and completion

The up and down arrow keys move through command history in an interactive Bash session. Press <code>Tab</code> to complete a command or path when the match is unique. Pressing it twice can show possible matches.

History files can contain commands and values you typed. Avoid entering passwords or secrets as command arguments because they may appear in process listings or shell history.

## Practice questions

1. Why is <code>cd</code> usually built into the shell?
2. What does <code>export</code> do to a variable?
3. What is <code>PATH</code> used for?
4. How do single quotes treat a variable name inside them?
5. Why should variable expansions usually be quoted?
6. What does the command substitution around <code>date +%F</code> return?
7. How does a question mark behave in a Bash filename pattern?
8. Why should secrets not be typed directly as command arguments?

## References

- [GNU Bash Reference Manual](https://www.gnu.org/software/bash/manual/)
- [Bash variables](https://www.gnu.org/software/bash/manual/html_node/Bash-Variables.html)
- [Bash shell expansions](https://www.gnu.org/software/bash/manual/html_node/Shell-Expansions.html)
- [Bash quoting](https://www.gnu.org/software/bash/manual/html_node/Quoting.html)
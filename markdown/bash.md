<!-- markdownlint-disable MD025 MD033 MD024 MD006 MD029-->

# My bash scripting Reference / Guide

This is mainly a references / Guide / Good Practices document for bash

Referenced from [Bash Academy](https://guide.bash.academy)

## Always try to quote arguments

Use `""` to allow expansion within the quotes

Use `''` to prevent expansion, and everywhere else where expansion isn't needed

```bash
# Example
username=' bob'
rm -vr /home/$username
# This deletes the enture home directory as the above
# Expands to 'rm -vr /home ' and 'rm -vr /home/bob'

rm -vr "/home/$username"
# Output: rm: cannot remove '/home/ bob': No such file or directory

# This ensures that the code is safer
```

## Redirection

Processes uses file descriptors(**FD**) to connect to streams. Each processes will generally have 3 standard file descriptors.

### Standard Redirection

*Standard Input **FD0***

*Standard Output **FD1***

*Standard Error **FD2***

Redirection is how you gain control of these streams

`>` is used to redirect the FDs, and redirects standard output by default

You can prepend the FD number to the `>` to redirect other FDs

```bash
# Example
ls -l a b c > myfiles 2> /dev/null
# Standard output(FD1) is redirected to myfiles
# Standard Error (FD2) is redirected to /dev/null
```

```visualization
The Visualization of the above
   ╭─────┴────╮
└─╼┥0  ls    1┝╾───╼ myfiles.ls
   │         2┝╾───╼ /dev/null
   ╰──────────╯
```

What if you want to merge the outputs of both output and error?

```bash
ls -l a b >myfiles.ls 2>&1 # Make FD 2 write to where FD 1 is writing
```

```visualization
The Visualization of the above
   ╭─────┴────╮
└─╼┥0  ls    1┝╾─┬─╼ myfiles.ls
   │         2┝╾─┘
   ╰──────────╯
```

This is known as copying file descriptors, copying one's file descriptor stream to another file descriptor.
> You can translate the syntax `2>&1` as Make FD `2` write(`>`) to where FD(`&`) `1` is currently writing.

```bash
# DO NOT DO THIS
ls -l a b 2>&1 >myfiles.ls
# This sets FD2's stream to the one FD1 is connected to at the time its running, which is probably the terminal
```

### File Descriptor Redirection Reference

#### File Redirection

```bash
# Syntax
[x] > file
# This makes FD x write to file
[x] < file
# This makes FD x read from file
```

#### File Descriptor Copying

```bash
# Syntax
[x]>&y
# Make FD x write to the stream of y
[x]<&y
# Make FD x read from the stream of y
```

#### Appending File redirection

```bash
# Syntax
[x] >> file
# Make FD x append to end of file
```

#### Redirecting standard output and standard error

```bash
# Syntax
&> file
# Make both FD1 and FD2 write to file
# Same as > file > 2>&1
# you can also append by &>> file
```

#### Here Documents

```bash
# Syntax
<<[-]delimeter
    here document
delimeter
# Make FD 0 read from the string between delimeters

# Example
cat <<.
Hello World.
Blah Blah Blah Blah Blah Blah Blah.
.
# You can prefix the << with - to tell bash to ignore tabs infront of heredoc. 
```

#### Here Strings

```bash
# Syntax
<<<string
# Make FD0 read from string
```

#### Closing File Descriptors

```bash
# Syntax
[x]>&-, [x]<&-
# Close FD x
```

#### Moving File Descriptors

```bash
# Syntax
[x]>&y-, [x]<&y-
# Replace FD x with FD y
```

#### Reading and Writing with a File Descriptor

```bash
# Syntax
[x] <> file
# Open FD x for both reading and writing to file

# Example
exec 5<>/dev/tcp/ifconfig.me/80
```

# Expansions

## Pathname Expansions

|Glob|Meaning|
|:--:|:--:|
|*|Matches any or no text|
|?|Matches 1 character|
|[characters]|matches a single character in the set|
|[[:classname:]]|matches any character in the set. List of sets<br> alnum, alpha, ascii, blank, cntrl, digit, graph, lower, print, punct, space, upper, word, xdigit|

To enable advanced glob patterns

```bash
shopt -s extglob
```
|Glob|Meaning|
|:--:|:--:|
|+(pattern)|Matches when pattern appears 1 or more times|
|*(pattern)|Matches when pattern appears 0 or more times|
|?(pattern)|Matches when pattern appears 0 or 1 times|
|@(pattern)|Matches when pattern appears once|
|!(pattern)|Matches when  none of the patterns in the list appear|

## Tilde Expansion

`~` expands to the users home directory

`~username` expands to the user's home directory. E.g. `~root` expands to `/var/root` on Mac.

## Commmand Substitution

`$(command)` runs the command in a subshell

Remember to **ALWAYS** put expansions in quotes(`""`). If unquoted, bash will split words, delete whitespaces, perform pathname expansion, etc, which is not required.

## Shell Variables

```bash
name=yadunut
echo "Hello, $name, How are you?"
```

### Assignment

Use `=` for assignment. **Do not use spaces** around the `=`. Spaces in bash have special meaning - they split commands into arguments.

### Parameter Expansion

We expand parameters by using the `$` symbol.

*Reminder: Parameters and all other expansions should __always__ be double quoted*

Allows you to wrap curly braces around expansion.

```bash
name=yadunut
time=10.00
echo "$name's current record is ${time}s
# yadunut's current record is 10.00s
```

Parameter Expansion Operators

```bash
name=yadunut
time=10.50
echo "$name's current record is ${time%./*} seconds and ${time#*.}milliseconds
# yadunut's current record is 10 seconds and 50 milliseconds
echo "PATH currently contains ${PATH//:/, }"
```

For the examples below, `url=https://ctf.yadunut.com/page.html`

| Operator                                                                                                                | Example         | Result                                                                              |
| :---------------------------------------------------------------------------------------------------------------------- | :-------------- | :---------------------------------------------------------------------------------- |
| `${parameter#pattern}`<br>Remove the **shortest** string that matches the `pattern` from the **beginning** of the value | `"${url#*/}"`   | `"https://ctf.yadunut.com/page.html"`<br>↓<br>`"/ctf.yadunut.com/page.html"`        |
| `${parameter##pattern}`<br>Remove the **longest** string that matches the `pattern` from the **beginning** of the value | `"${url##*/}"`  | `"https://ctf.yadunut.com_age.html"<`br>↓<br>`"page.html"`                          |
| `${parameter%pattern}`<br>Remove the **shortest** string that matches the `pattern` from the **end** of the value       | `"${url%/*}"`   | `"https://ctf.yadunut.com/page.html"`<br>↓<br>`"https://ctf.yadunut.com"`           |
| `${parameter%%pattern}`<br>Remove the **longest** string that matches the `pattern` from the **end** of the value       | `"${url%%/*}"`  | `"https://ctf.yadunut.com/page.html"`<br>↓<br>`"https:"`                            |
| `${parameter/pattern/replacement}`<br>Replace the **first** string that matches `pattern` with `replacement`            | `"${url/./-}"`  | `"https://ctf.yadunut.com/page.html"`<br>↓<br>`"https://ctf-yadunut.com/page.html"` |
| `${parameter//pattern/replacement}`<br>Replace the **each** string that matches `pattern` with `replacement`            | `"${url//./-}"` | `"https://ctf.yadunut.com/page.html"`<br>↓<br>`"https://ctf-yadunut-com/page-html"` |
| `${parameter//pattern/replacement}`<br>Replace the **each** string that matches `pattern` with `replacement`            | `"${url//./-}"` | `"https://ctf.yadunut.com/page.html"`<br>↓<br>`"https://ctf-yadunut-com/page-html"` |

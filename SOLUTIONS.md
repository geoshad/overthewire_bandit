# Solutions

My notes on overthewire.org/wargames/bandit.

Each level requires privilege escalation in order to escalate to the next level, often by accessing a password in one way or another.

## Level 0 

Solving Level 0 involved SSH'ing into the host, bandit.labs.overthewire.org, on port 2220, as the user bandit0, using the password bandit0.

```bash
> ssh bandit0@bandit.labs.overthewire.org -p 2220 
> bandit0
```

## Level 0 → 1

Escalating to Level 1 involved investigating the current directory and surrounding files, and printing the contents of the readme file, which contained the password to the next level.

```bash
> pwd
> ls
> cat readme
NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL
```

## Level 1 → 2

Escalating to Level 2 involved printing the contents of a file with an unorthodox filename.

```bash
> cat ./-
rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi
```

## Level 2 → 3

Escalating to Level 3 involved printing the contents of a file that had spaces in its filename. Single quotes were used to distinguish the filename.

```bash
> cat 'spaces in this filename'
aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG
```

## Level 3 → 4

Escalating Level 4 involved printing the contents of a hidden file. To do this, we used the `-a` flag with `ls` which will display all files.

```bash
> cd inhere/
> ls -a
> cat .hidden
2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe
```

## Level 4 → 5

Escalating Level 5 involved finding a human-readable file in a directory, and printing its contents. This file also had an unorthodox filename, which needed extra syntax in order to print.

```bash
> cd inhere/
> find . -type f | file -f -
> cat ./-file07
lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR
```

## Level 5 → 6

Escalating to Level 6 involved finding a file with the following properties: human-readable, 1033 bytes in size, and not executable.

```bash
> cd inhere/
> find . -size 1033c
> cd maybehere07/
> cat ./.file02
P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU
```

## Level 6 → 7

Escalating to Level 7

```bash
> find / -group bandit6 -size 33c -user bandit7 -type f 2>/dev/null
> cat /var/lib/dpkg/info/bandit7.password
z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S
```



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

Escalating to Level 2 involved printing the contents of a file with an unorthodox filename. To be distinguished, this filename required the relative filepath, `./`, to be included. Otherwise, the command `cat -` would be treated as if it is awaiting standard input.

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

Escalating to Level 7 involved finding a file with the following properties: owned by user bandit7, owned by group bandit6, and 33 bytes in size. Searching for this file displays many warnings, which can be 'thrown to the void' by using `2>/dev/null`, thus revealing the true location of the next password.

```bash
> find / -group bandit6 -size 33c -user bandit7 -type f 2>/dev/null
> cat /var/lib/dpkg/info/bandit7.password
z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S
```

## Level 7 → 8

Escalating to Level 8 involved finding the password in a file, next to the word 'millionth'.

```bash
> cat data.txt | grep millionth
TESKZC0XvTetK0S9xNwm25STk5iWrBvP
```

## Level 8 → 9

Escalating to Level 9 involved finding the password in a file, which was the only line of text occuring only once. This was done by filtering for the unique line after sorting them, by using `uniq` with the `-u` flag.

```bash
> sort data.txt | uniq -u
EN632PlfYiZbn3PhVK3XOGSlNInNE00t
```

## Level 9 → 10

Escalating to Level 10 involved printing the password, which was a human-readable string preceded by several '=', from a file of mainly unreadable symbols. This was done by printing readable characters using `strings`, and `grep`ing the strings preceded by '='.

```bash
> strings data.txt | grep ===
G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s
```

## Level 10 → 11

Escalating to Level 11 involved decoding and printing the password from `data.txt`, which contained base64 encoded data. The data can be decoded with the `base64` command with the `-d` flag.

```bash
> base64 -d data.txt
6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM
```

## Level 11 → 12

Escalating to Level 12 involved decoding and printing the contents of a file, wherein its letters had been rotated 13 positions (ROT13). In order to rotate the letters back to normal, the contents of `data.txt` was passed through the `tr` command, revealing the translated text.

```bash
> cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv
```

## Level 12 → 13

Escalating to Level 13 involved ..

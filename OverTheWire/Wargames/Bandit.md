# Bandit 0
Zugriff: `ssh bandit0@bandit.labs.overthewire.org -p 2220`
Passwort: `bandit0`

### Aufgabe: 
>The password for the next level is stored in a file called **readme** located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.

### Lösung:
Benötigte commands: `ls`, `cat` 
```bash
bandit0@bandit:~$ ls
readme
bandit0@bandit:~$ cat readme
boJ9jbbUNNfktd78OOpsqOltutMc3MY1
```
# Bandit 1
Zugriff: `ssh bandit1@bandit.labs.overthewire.org -p 2220`
Passwort: `boJ9jbbUNNfktd78OOpsqOltutMc3MY1`

### Aufgabe: 
>The password for the next level is stored in a file called **-** located in the home directory in the home directory

### Lösung:
Benötigte commands: `ls`, `cat` 
```bash
bandit1@bandit:~$ ls
-
bandit1@bandit:~$ cat ./-
CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9
```

# Bandit 2

Zugriff: `ssh bandit2@bandit.labs.overthewire.org -p 2220`
Passwort: `CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9`

### Aufgabe: 
>The password for the next level is stored in a file called **spaces in this filename** located in the home directory

### Lösung:
Benötigte commands: `ls`, `cat` 
```bash
bandit2@bandit:~$ ls
spae
bandit2@bandit:~$ cat "spaces in this filename"
UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK
```

# Bandit 3

Zugriff: `ssh bandit3@bandit.labs.overthewire.org -p 2220`
Passwort: `UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK`

### Aufgabe: 
>The password for the next level is stored in a hidden file in the **inhere** directory.

### Lösung:
Benötigte commands: `ls`, `cat` 
```bash
bandit3@bandit:~$ ls -a ./inhere
.hidden
bandit3@bandit:~$ cat inhere/.hidden
pIwrPrtPN36QITSp3EQaw936yaFoFgAB
```

# Bandit 4

Zugriff: `ssh bandit4@bandit.labs.overthewire.org -p 2220`
Passwort: `pIwrPrtPN36QITSp3EQaw936yaFoFgAB`

### Aufgabe: 
>The password for the next level is stored in the only human-readable file in the **inhere** directory. Tip: if your terminal is messed up, try the “reset” command.

### Lösung:
Benötigte commands: `cd`, `cat`, `file` 
```bash
bandit4@bandit:~$ cd inhere
bandit4@bandit:~/inhere$
bandit4@bandit:~/inhere$ file ./-file*
./-file00: data
./-file01: data
./-file02: data
./-file03: data
./-file04: data
./-file05: data
./-file06: data
./-file07: ASCII text
./-file08: data
./-file09: data
bandit4@bandit:~/inhere$ cat ./-file07
koReBOKuIDDepwhWk7jZC0RTdopnAYKh
```

# Bandit 5

Zugriff: `ssh bandit5@bandit.labs.overthewire.org -p 2220`
Passwort: `pIwrPrtPN36QITSp3EQaw936yaFoFgAB`

### Aufgabe: 
>The password for the next level is stored in a file somewhere under the **inhere** directory and has all of the following properties:
-   human-readable
-   1033 bytes in size
-   not executable

### Lösung:
Benötigte commands: `cd`, `cat`, `find` 
```bash
bandit4@bandit:~$ cd inhere
bandit4@bandit:~/inhere$
bandit4@bandit:~/inhere$ find -size 1033c
./maybehere07/.file2
bandit4@bandit:~/inhere$ cat maybehere07/.file2
koReBOKuIDDepwhWk7jZC0RTdopnAYKh
```

# Bandit 19

Zugriff: `ssh bandit19@bandit.labs.overthewire.org -p 2220`
Passwort: `koReBOKuIDDepwhWk7jZC0RTdopnAYKh`

### Aufgabe:

> To gain access to the next level, you should use the setuid binary in the homedirectory. Execute it without arguments to find out how to use it.evel can be found in the usual place (/etc/bandit_pass), after you have used the setuid binary.

### Lösung:
Benötigte commands: `cat`
```bash
bandit19@bandit:~$ ./bandit20-do cat /etc/bandit_pass/bandit20
GbKksEFF4yrVs6il55v6gwY5aVje5f0j
```

# Bandit 20

Zugriff: `ssh bandit20@bandit.labs.overthewire.org -p 2220`
Passwort: `GbKksEFF4yrVs6il55v6gwY5aVje5f0j`

### Aufgabe:

> There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).
**NOTE:** Try connecting to your own network daemon to see if it works as you think

### Lösung:
Benötigte commands: `nc`

Client 1:
```bash
bandit20@bandit:~$ ./suconnect 10000
Read: GbKksEFF4yrVs6il55v6gwY5aVje5f0j
Password matches, sending next password
```
Client 2:
```bash
bandit20@bandit:~$ nc -lvn 127.0.0.1 -p 10000
listening on [any] 10000 ...
connect to [127.0.0.1] from (UNKNOWN) [127.0.0.1] 40788
GbKksEFF4yrVs6il55v6gwY5aVje5f0j
gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr
```

# Bandit 21
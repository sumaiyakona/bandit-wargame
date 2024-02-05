# OverTheWire_bandit-wargame
**Bandit** is one of the wargames focusing on linux basics for beginners such as ssh, telnet, cronjob and many more by the brillint **Over The Wire** team; can be found: https://overthewire.org/wargames/bandit/bandit0.html in here.<br>

I'll be seen here solving the levels one after another with a very clear objective leart with solving each one of them. Let's start!<br>

## Level 0
Goal: Logging into the game using SSH.

Given,<br>
Host: bandit.labs.overthewire.org<br>
Port: 2220<br>
Username: bandit0<br>
Password: bandit0<br>

Simply type `ssh bandit0@bandit.labs.overthewire.org -p 2220` to connect with the host using ssh.

## Level 0 → Level 1
Goal: Looking into files for password/flag and logging in using ssh for the next level.

Type, `ls` and then, `cat readme` to look for the flag and login.

## Level 1 → Level 2
Goal: Reading 'dashed filename'.

In this case, the option '<' before the dash (-) file is needed to specify: `cat < -` or `cat <-`.

## Level 2 → Level 3
Goal: Reading files named with 'spaces'

To read any file with spaces, just lock it with an apostrophe as shown: `cat 'spaces in this filename'`. Putting backslash before each works as well: `cat spaces\ in\ this\ filename`.

## Level 3 → Level 4
Goal: Reading from a hidden file.

What we need to know in here is, hidden files typically start with a dot(.) and as a result cannot be seen with the `ls` command. To see hidden files in linux, `-a` switch is used. Hence, typing `ls -la` to view all the hidden files and rest will be the following: `cat .hidden`.

## Level 4 → Level 5
Goal: Spotting human readable files.

Note: human-readable file means a file with only ASCII text in this context which we can clearly see in the screenshot below when used the command `file ./-file*`.

<img width="859" alt="Screenshot 2024-01-30 at 10 29 05 pm" src="https://github.com/sumaiyakona/bandit-wargame/assets/31168741/ef7df512-589e-47df-b371-c9eca0e0bbaa">

Now simply read the file `cat ./-file07`

## Level 5 → Level 6
Goal: Finding a targeted file given a set of properties, by using the find command. So, the password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:<br>
**human-readable<br>
1033 bytes in size<br>
not executable<br>**

Therefore, the command to find the targeted file `find -type f -readable ! -executable -size 1033c` & then `cat maybehere07/.file2`.

## Level 6 → Level 7

Goal: Finding a targeted file given a set of properties, by using the find command (similar to previous one, except with a different set of search criteria).

The password for the next level is stored somewhere on the server and has all of the following properties:<br>
**owned by user bandit7<br>
owned by group bandit6<br>
33 bytes in size<br>**

Note: Since it is stated that the password is stored somewhere on the server, we must first navigate to the root folder. `cd ..` twice from the home directory, and then pwd to verify that we are in the root directory. We should only see the slash ('/') character from running pwd and then type `find -user bandit7 -group bandit6 -size 33c`
    
Note: There are a lot of files which match the given property, but all of these files (except one) cannot be accessed, as seen from the string of "Permission denied" messages displayed. Only one search result does not have this message and that's the following one:<br>
    
    File: /var/lib/dpkg/info/bandit7.password

Finally, `cat /var/lib/dpkg/info/bandit7.password`.

## Level 7 → Level 8

Goal: Searching for a specific word within a file, by using the grep command.

The password for the next level is stored in the file data.txt next to the word millionth.
So, the command should be `grep millionth data.txt` & voila!
    
## Level 8 → Level 9

Goal: Searching within a file given a set of criteria, by using the sort and uniq commands, in addition to piping within the terminal.

The password for the next level is stored in the file data.txt and is the only line of text that occurs only once.
In this case, `cat data.txt | sort | uniq -u`
Note: -u argument indicates to print only the unique lines.
    
## Level 9 → Level 10
## Level 11 → Level 12
## Level 12 → Level 13
## Level 13 → Level 14
## Level 14 → Level 15

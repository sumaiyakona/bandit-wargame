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
In this case, `cat data.txt | sort | uniq -u`; -u argument indicates to print only the unique lines.
    
## Level 9 → Level 10

Goals: Searching for strings within a file that does not contain only ASCII characters, by using the strings and grep command.

The password for the next level is stored in the file data.txt in one of the few human-readable strings, beginning with several ‘=’ characters.
Note: file data.txt tells us that the file is a data file, and does not contain only ASCII text. Hence, it was mentioned that there are only a few human-readable strings which is why the command should be `strings data.txt | grep ===`
    
## Level 11 → Level 12

Goals: Learning to decode base64 encoded data, using the base64 command.

The password for the next level is stored in the file data.txt, which contains base64 encoded data.
So, simply it is `base64 -d data.txt`; -d argument indicates decoding of data.
    
## Level 12 → Level 13

Goals: Learning to transform strings, using the tr command.

The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions. So, the command is `cat data.txt | tr A-Za-z N-ZA-Mn-za-m`
Note: Inverted commas or square brackets around the parameters of the tr command are not required.
    
## Level 13 → Level 14

Goals: Learning to convert hexdump files and extract compressed files, using the xxd and various (de)compression utility commands respectively.

The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work using mkdir. For example: mkdir /tmp/myname123. Then copy the datafile using cp, and rename it using mv (read the manpages!).

    Step 1: First, make a new directory of your choice under /tmp. Next, copy data.txt to this new directory. There is no need to rename it in my opinion since I felt that I had to remember one more different file name to keep track of where I started.
    Step 2: The file command would state data.txt as a file with ASCII text, but if you view the file contents, it is actually a hex dump. Command to convert the hexdump into binary: xxd -r data.txt > newdata.txt
    Step 3: file newdata.txt shows us that the converted hexdump contains gzip compressed data. Using gunzip to unzip the gzip compressed data gives an error of unknown suffix -- ignored, because the file extension is .txt, which does not match what gunzip is looking for (which is .tar.gz). Hence, rename the file with mv newdata.txt newdata.tar.gz. Then, run gunzip newdata.tar.gz, which gives newdata.tar.
    Step 4: file newdata.tar shows us that the file was compressed with bzip2. However, this file extension does not match what bunzip2 is looking for (which is .bz2). Hence, rename the file with mv newdata.tar newdata.bz2. Then, run bunzip2 newdata.bz2, which gives newdata.
    Step 5: file newdata shows us that the file was compressed with gzip. Rename the file using mv newdata newdata.tar.gz to give the file the appropriate file extension. Run gunzip newdata.tar.gz to get newdata.tar.
    Step 6: file newdata.tar shows us that the file was compressed with POSIX tar. Run tar -xf newdata.tar to get data5.bin. The -x parameter tells tar to extract the files, while the -f parameter tells tar the name and path of the compressed file.
    Step 7: file data5.bin shows us that the file was compressed with POSIX tar. Run tar -xf data5.bin to get data6.bin.
    Step 8: file data6.bin shows us that the file was compressed with bzip2. Rename the file with mv data6.bin data6.bz2. Run bunzip2 data6.bz2 to get data6.
    Step 9: file data6 shows us that the file was compressed with POSIX tar. Run tar -xf data6 to get data8.bin. No need to rename data6 to data6.tar before running the tar command.
    Step 10: file data8.bin shows us that the file was compressed with gzip. Rename the file using mv data8.bin data8.tar.gz. Run gunzip data8.tar.gz to get data8.tar.
    Step 11: file data8.tar shows us that the file contains only ASCII text, which is the password to the next level.
    File: data8.tar

## Level 14 → Level 15

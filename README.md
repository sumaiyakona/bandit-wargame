# bandit-wargame
**Bandit** is one of the wargames focusing on linux basics for beginners such as ssh, telnet, cronjob and many more by the brillint **Over The Wire** team; can be found: https://overthewire.org/wargames/bandit/bandit0.html in here.<br>

I'll be seen here solving the levels one after another with a very clear objective leart with solving each one of them. Let's start!<br>

## Level 0
Goal: Logging into the game using SSH.

Given,
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

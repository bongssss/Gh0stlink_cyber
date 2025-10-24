
Password to bandit1:  ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If  

Password for bandit2: 263JGJPfgU6LtdEvgfWU1XP5yac29mFx

Password for bandit3: MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx

Password for bandit4: 2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ

Password for bandit5: 4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw

Password for bandit6: HWasnPhtq9AVKe0dmk45nxy20cvUa6EG

Password for bandit 7: morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj

Password for bandit8 : dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc

Password for bandit9: 4CKMh1JI91bUIZZPXDqGanal4xvAg0JM

Password for bandit10 : FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey

Password for bandit11: dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr

Password forbandit12  : 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4

Password for bandit13; FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn

Password for bandit14: sshkey.private , password : MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS

Password for bandit15: 8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo (using the netat to  command to submit current password of bandit14 to get bandit15 password)

Password for bandit 16:kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx

Password to bandit 17: ssh -i private16.key bandit17@bandit.labs.overthewire.org -p 2220

Bandit 18 password:  x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO

Bandit 19 password: cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8

pasword to bandit 20: 0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO


Password to bandit level 21: EeoULMCra2q0dSkYj561DX7s1CpBuOBt

password for bandit 22:
tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q

password for bandit 23:





  

  

  

  

  **Documentation about how to beat all the levels**

  

**Level0:** 

The instruction is to login to the remote host using the **ssh protocol** . I used the ssh **bandit0@bandit.labs.overthewire.org -p 2220**

  

 **bandit0 -**  remote host username 

**@bandit.labs.overthewire.org -**  remote host domain 

**-p 2220 -**  signifies the port with which to establish the ssh connection to the remote host 

  

To find the password to the next level, I used the **cat readme**  command which allows me to  read the contents of the readme file in the terminal and find the password.

  

  

**Level1 -> Level2**

  

The instruction is to login using ssh and retrieve the password to the next level from the file named “-” I used the **cat ./-**  command to read the file and find the password.

  

**Level2 -> Level3**

  

 I logged in to the level2 and to retrieve the password from the file names “spaces in this filename” I use the **cat spaces\ in\ this\ filename** command or **cat ‘spaces in this filename’**

  

**Level3 -> level4**

  

I logged in the level3 and am supposed to retrieve the password from a hidden file in the  **inhere** directory. I found the hidden file using the **ls -la**  command and used the  **cat**  command 

  

**Level4 -> Level5**

  

 To access the level5 password, I have to find the only human-readable file in the  **inhere** directory. I use the  **cat ./-file** command to read all the files and I found the password in the **-file07** 

  

**Level5 -> level6**

  

The password for the next level is stored in a file somewhere under the **inhere** directory and has all of the following properties:

- human-readable
- 1033 bytes in size
- not executable

 I used the  **file */{.,}* | grep "ASCII text" | grep -v ", with very long lines" | du -b -a | grep 1033**  command  to find the exact file.

  

**file -** returns specified filetypes

***/* -** searches for all the files in all the directories under **inhere**

**{.,} -**  the brackets include  **‘.’** For hidden files and ‘**,’**  for all other file types

 **| -** passes the output to the next set of commands

 **grep -**  searches for patterns in a file, could be a particular string in a particular file or a pattern (in this case, human readability) in a group of files. Thus  **grep “ASCII text”**  looks for files that contain human readable text and  **grep -v “with very long lines”**  excludes the phrase ‘**with very long lines’** 

**du -**  returns the file size(es)  **-b**  means in bytes and **-a**  means all so this command returns all the file sizes and pipes them (**|**) through to the final **grep** command which selects the file with a size of **1033** bytes.

  

  

**Level6 -> level7**

  

 I used the  **file / -type f -user** 

  

**Level8 -> level9**

  

**Level9 -> Level10**

  

**Level11 -> Level12**

  

**Level12 -> Level13**

**Level13 -> Level14**

**Level 19 -> level 20**

 A **setuid binary** is a special type of executable program on Unix-like operating systems (like Linux) that, when executed, runs with the **privileges of the file's owner** rather than the privileges of the user who launched it.

The name stands for "**Set User ID upon execution**".

### The Problem It Solves: Privilege Escalation

On a multi-user system, there are tasks that require higher privileges (e.g., root privileges) that ordinary users should not normally have. For example:

- Changing your password (modifying `/etc/shadow`, which is readable only by root).
- Using the `ping` command (which requires raw network sockets, a privileged operation).
- Shutting down the system from a user's session.

Instead of giving every user the root password, the system uses setuid binaries. A privileged program (owned by root) is created to perform the specific task safely. The `setuid` mechanism allows a regular user to _temporarily_ become root _only for the duration of that specific program's execution_.  

![[bandit 20 solution.png]]


**level20 -> level21**

1. Using ’netcat’, we can create a connection in server mode - which listens for inbound connection. To have netcat send the password, I use echo and pipe it into netcat. The `-n` flag is to prevent newline characters in the input. 
![[Bandit21A.png]]

2. Running the setuid binary with port 1234 means it will connect to our netcat server, receive the password inputted through `echo` and sends back the next password.

![[bandit21B.png]]




**level21 -> level22**
in this level  cronjobs are made use of. cronjobs are programs running automatically at regular intervals. In Linux, there are multiple folders that can contain these cronjobs: cron.d, cron.daily, cron.hourly, cron.monthly, crontab, cron.weekly. The folders contain files with instructions on how the programs are run. It starts with the first five columns, which indicate at what time/interval the program should be done. Next is the command/program that is to be executed.

![[bandit22.png]]


level 22 -> level 23


![[Bandit23a.png]]


![[Bandit23b.png]]
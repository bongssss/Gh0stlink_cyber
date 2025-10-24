- sudo privileges
- suid privileges
- privileged groups 
- capabilities
- cron jobs - executing tasks at a specific time by running scripts of binaries can be found in `/etc/crontab`
- 

three things to check for
reading sensitive files
writing to sensitive files
executing commands with another users credentials
`find / -type f or -type d -perm -4000`

`G - 6000`
`S - 4000`
>2 /dev/null


gtfobins.github.io - 

### Capstone project
- exploit vulnerable machine using the whole pen testing suit
- port scan
- find vulnerabilities 
- exploit them
- 
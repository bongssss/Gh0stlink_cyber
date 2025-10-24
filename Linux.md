
# Linux Fundamentals I

## Introduction

The name "Linux" is actually an umbrella term for multiple OS's that are based on UNIX (another operating system). Thanks to UNIX being open-source, variants of Linux comes in all shapes and sizes - suited best for what the system is being used for.

For example, Ubuntu & Debian are some of the more commonplace distributions of Linux because it is so extensible. I.e. you can run Ubuntu as a server (such as websites & web applications) or as a fully-fledged desktop. For this series, we're going to be using Ubuntu.

The first version of linux was released in 1991.

***

## Commands

<table><thead><tr><th width="199">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>echo</code></td><td>Output text</td></tr><tr><td><code>whoami</code></td><td>Find out which user we are currently logged into</td></tr><tr><td><code>ls</code></td><td>List the folder or directories</td></tr><tr><td><code>cd</code></td><td>Change directory</td></tr><tr><td><code>cat</code></td><td>Concatenate the contents of a file</td></tr><tr><td><code>pwd</code></td><td>Print the working directory</td></tr><tr><td><code>clear (ctrl+l)</code></td><td>Clear the screen</td></tr><tr><td><code>find</code></td><td>Finds hidden folder and can specify a parameter with -name (e.g. find -name *.txt)</td></tr><tr><td><code>grep</code></td><td>Searches the contents of files for specific values</td></tr></tbody></table>

***

## An Introduction To Shell Operators

<table><thead><tr><th width="201">Symbol / Operator</th><th>Description</th></tr></thead><tbody><tr><td><code>&#x26;</code></td><td>Allows you to run commands in the background of your terminal</td></tr><tr><td><code>&#x26;&#x26;</code></td><td>Allows you to combine multiple commands together in one line of the terminal and running both commands if the first runs</td></tr><tr><td><code>></code></td><td>It is a redirector (we can take the output from a command and direct it elsewhere - using cat)</td></tr><tr><td><code>>></code></td><td>The same function as > but appends the output rather than replacing (nothing is overwritten)</td></tr></tbody></table>



Yesterday, I spoke about network services and network protocols. I mentioned some of the most frequently used protocols and that fact that they are able to send and receive data in form of packets through channels known as  'well known' ports.

The fact that that these network protocols are the most frequently used i.e., HTTP & HTTPs, opens them up to attacks by malicious actors who try to exploit some of the well known vulnerabilities associated with these protocols.

so how do we defend against these attacks, explore these vulnerabilities and monitor what happens on networks? 
 We are able to do this with the use of LINUX OS. 
 
 LINUX is an Operating System that OS's that is based on UNIX with many variants that come in all shapes and sizes and for different use cases. These different versions are known as distributions or 'distros'. A LINUX distro that is relevant for cybersecurity and exploitation analysis is Kali Linux because it comes with all the necessary tools and frameworks that are most used in penetration testing such as Wireshark, Burp Suite, Metasploit and Nmap.
 
the LINUX shell/command line interface makes use of command and operators that can be used for core system operations within the operating system itself as well as for interaction with the various tools and frameworks useful for exploitation analysis.

In the next summary, I'll go over how these tools available on Kali Linux as well as linux command and operators can be used to perform basic operations i.e., modifying user permissions on files and directories as well as perform operations related to exploitation analysis such as scanning a network.

## Common Directories


`/etc`

The etc folder (short for etcetera) is a commonplace location to store system files that are used by your operating system.

`/var`

The var folder (short for variable data) stores data that is frequently accessed or written by service or applications running on the system. For example, log files (/var/log).

`/root`

The home for the root user.

`/tmp`

Short for temporary, the directory is volatile and is used to store data that is only needed to be accessed once or twice. Similar to RAM on a computer.

`nano`

Edit or create a file

`wget`

Download files from the web via HTTP

`scp`

Copy files & directories from your current system to a remote system and vice versa

where would we look if we wanted to exploit specific software?
The answer to that question lies in websites such as 
- [ExploitDB](https://www.exploit-db.com/)
    
- [NVD](https://nvd.nist.gov/vuln/search)
    
- [CVE Mitre](https://cve.mitre.org/)

Kali comes pre-installed with a tool called "searchsploit" which allows you to search ExploitDB from your own machine. This is offline, and works using a downloaded version of the database, meaning that you already have all of the exploits already on your Kali Linux!

## Web shells 
A browser-based web session used to interact with the underlying OS of a web server( basically the host or system that stores the data displayed by a web browser)
- to gain remote code execution access, we must find a web application vulnerability that gives or enables file upload capabilities as
- most web shells are gained when a payload that grants remote code execution within a web browser and was written in a web language is successfully sent to a target web server

### Types of Web shells 
- #### Laudanum shells 
Laudanum is a repository of files that can be used to gain backdoor access to a target via a reverse shell. it can be used to run commands on the target host right from the web browser and do much more. It includes injectable files for different web browsers written in different web languages
 the laudanum files can be found int */usr/share/laudanum* part of your kali linux machine.
![[Laudanum web shell fiies.png]]




For most of the files within Laudanum, you can copy them as-is and place them where you need them on the victim to run. 

For specific files such as  **shells**, you must edit the file first to insert your `attacking. host IP address`  to ensure you can access the web shell or receive a callback in the instance that you use a reverse shell. Before using the different files, be sure to read the contents and comments to ensure you take the proper actions.


LAMP stack : A web app that uses
Linux OS
Apache web server
MySQL database
PHP programming language (interchangeable with Perl/Python)
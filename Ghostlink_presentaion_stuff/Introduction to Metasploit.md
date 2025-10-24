### Good to know 
- Metasploit is built on ruby and consists of modules 
- It is a penetration testing framework that helps with creating running and testing exploits as well as testing security flaws, listing networks, lunching attacks and avoiding detection
- it contains a database of already found exploits in the form of modules 
- considered as an exploitation Swiss army knife for its applicability to multiple penetration testing use cases

### Metasploit Console (MSFConsole)
- Generally the most widely used Metasploit interface
- you can gain easy access to most metasploit features through it
- it is also a stable msf interface 
- allows for execution of eternal commands 


### Metasploit MSFConsole Architecture 
- location of the base files for metasploit is */usr/share/metasploit-framework*  on kali linux
-  Data, Documentation & Lib are the base files for the Framework. The Data and Lib are the functioning parts of the **msfconsole** interface, while the Documentation folder contains all the technical details about the  metasploit project.
-  The modules folder splits metasploit modules into different categories(folders)
- Plugins folder offers a pentester  flexibility when using the `msfconsole` since it contains metasploit plugins that can easily be manually or automatically loaded as needed to provide extra functionality and automation during our assessment of a target.
- the scripts folder includes the meterpreter functionality as well as others
- tools file contains command line utilities that can be called directly from the msfconsole menu.
- ![[Metasploit framework image.png]]
### Navigating the MSFConsole 
- start by typing **msfconsole** into any kali linux terminal 
![[MSFConcole start.png]]

- Once we are in the `msfconsole`, we can select from an extensive list containing all the available Metasploit modules. Each of them is structured into folders, which will look like this: 

`**<No.> <type>/<os>/<service>/<name>**`

For example:

794   exploit/windows/ftp/scriptftp_list
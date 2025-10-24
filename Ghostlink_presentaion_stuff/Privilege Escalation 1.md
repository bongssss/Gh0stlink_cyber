Privilege escalation is the exploitation of a vulnerability, design flaw, or configuration oversight in an operating system or application to gain unauthorised access to resources that are usually restricted from the users. Essentially going from a lower permission account to a higher one or in the ideal case the account with root privileges.

Privilege escalation is crucial because it lets you gain system administrator levels of access, which allows you to perform actions such as:

- Resetting passwords  
- Bypassing access controls to compromise protected data
- Editing software configurations
- **Enabling persistence**
- **Changing the privilege of existing (or new) users**
- Execute any administrative command



### Steps to follow in P-ESC

https://tryhackme.com/room/linprivesc
1. **Enumeration**
Enumeration is the first step you have to take once you gain access to any system

Several tools can help you save time during the enumeration process. These tools should only be used to save time knowing they may miss some privilege escalation vectors. Below is a list of popular Linux enumeration tools with links to their respective Github repositories.

The target system’s environment will influence the tool you will be able to use. For example, you will not be able to run a tool written in Python if it is not installed on the target system. This is why it would be better to be familiar with a few rather than having a single go-to tool.

    LinPeas: https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/linPEAS
    LinEnum: https://github.com/rebootuser/LinEnum
    LES (Linux Exploit Suggester): https://github.com/mzet-/linux-exploit-suggester
    Linux Smart Enumeration: https://github.com/diego-treitos/linux-smart-enumeration
    Linux Priv Checker: https://github.com/linted/linuxprivchecker 


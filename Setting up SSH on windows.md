---
title: Setting up SSH on windows
tags: []
description: SSH is used to run cmd and powershell on a remote PC. 1. Install the
  SSH server on the server. Follow the powershell rules here . Then turn on the…
created: '2024-12-11'
modified: '2024-12-17'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Setting%20up%20SSH%20on%20windows.aspx
---

SSH is used to run cmd and powershell on a remote PC.
  

1\. Install the SSH server on the server. [Follow the powershell rules here](https://learn.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse?tabs=powershell&pivots=windows-server-2022#install-openssh-for-windows-server). Then 
 [turn on the 1password ssh agent](https://developer.1password.com/docs/ssh/get-started#step-3-turn-on-the-1password-ssh-agent), and add the following to your 
 [1pass ssh config file](https://developer.1password.com/docs/ssh/agent/config) (default path is "C:\\Users\\\<your user \>\\AppData\\Local\\1Password\\config\\ssh\\agent.toml") to use all ssh keys from 1pass:   

  
`![Screenshot 2024-12-17 103233.png](images/PublishingImages_Pages_Setting_up_SSH_on_windows_Screenshot_2024-12-17_103233.png)`

  

2\. Generate a public private key pair. In 1pass, new item \> ssh key \> add private key \> generate new. Save it. In the same item, add details about the server address, port, and command used to log in. See the other ssh keys in 1pass for an example. You can also add a "related item" wihch is the server details, if there is already a 1pass item for that server.
  

3\. Deploy to the remote server
  

This assumes you want to log in as the admin account. If you don't want the admin account, see here: https://learn.microsoft.com/en\-us/windows\-server/administration/openssh/openssh\_keymanagement\#standard\-user
  

Copy the public key from the 1pass ssh item you just created. It will look look something like:
  

ssh\-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIENp9CwaLKREa2hct3csg92UFOAVEtFFK5AXaDvqngYC kurren@DESKTOP\-RJQ9FCI
  

Log into the remote server via RDP or another method. Create a text file at C:\\ProgramData\\ssh\\administrators\_authorized\_keys (no file extension). Open in notepad, paste the text you previously copied, save and close.
  

4\. Set the file you just created so that only admins can access it. In powershell on the server:
  

icacls.exe "C:\\ProgramData\\ssh\\administrators\_authorized\_keys" /inheritance:r /grant "Administrators:F" /grant "SYSTEM:F"
  

5\. Test the connection from your local pc:
  

ssh username@PCNAME
  

It should open up a cmd. Type powershell to open a powerhell. Use exit to exit the powershell, then exit again to exit the cmd and end the ssh.
  

6\. Disable ssh password authentication on the server. On the server, go to "C:\\ProgramData\\ssh\\sshd\_config", add these lines at the top:
  

PasswordAuthentication no
PermitRootLogin prohibit\-password
authenticationmethods publickey
  

7\. If you want to expose the ssh to the internet, go to the draytek router configuration: https://router.codis.co.uk:8443/ (credeentials are in 1pass). NAT \> Port Redirection \> Add. 
  

\- Profile: PC Name followed by SSH. eg CD01DT10023SSH
\- Enable: yes
\- Port redirection mode: one to one
\- WAN Profile: ALL
\- Protocol: TCP/UDP
\- Public Port: The number 5 \+ a random 4 digits. Eg: 59218\. Make sure it isn't already in use.
\- Private IP: Local network IP of the pc
\- Private Port: 22 (this is the port of SSH)
  

Apply
  

You can then test the connection by doing 
  

ssh username@81\.99\.115\.224 \-p \<port\> 
  

eg:
  

ssh localadmin@81\.99\.115\.224 \-p 6191

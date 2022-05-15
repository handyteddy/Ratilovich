---
layout: post
title: TryHackMe - GamingServer
categories: thm
permalink: /:categories/gamingserver/
---

The hack starts with simple port scan 
`Nmap- -sC -sV <machine IP> -oN Default_Scan.txt`

<img src="/assets/images/gamingserver/nmap.png" height="100%" width="100%">

The only quick vector for information is port 80 (HTTP) and port 22 (SSH) for attack
A quick look at the web page hosted at 80 `http://<machine_ip>` give us a gaming portal with no much information on the front end

<img src="/assets/images/gamingserver/homepage.png" height="100%" width="100%">



but a usually important `view-source:<machine_ip>` reveals what to seems to be a username which we store in a text file for later use

<img src="/assets/images/gamingserver/source.png height="100%" width="100%">


**Web enumeration** continued with the “holy Dirbuster” or “ heavenly gobuster” as you please, reveals multiple directories along with

- Dic.lst [seems to be a simple wordlist , should to be downloaded]
- Secretkey [which seems to be private key, should be downloaded]
- Manifesto.txt [very useless manifesto that’s only there to teach you poetry ]

<img src="/assets/images/gamingserver/dirbuster.png height="100%" width="100%">

We have a USERNAME and what seems to be an SSH key, nothing stops us from logging into the server using SSH, since the SSH protocol allows the use of SSH keys to authenticate,
so long we set the permissions of the private key file to 600 by doing ```console chmod 600 id_rsa```
First we set the permission and secondly we log in


`“ssh -i secret_key john@<machine_ip>“ should kick us in`

<img src="/assets/images/gamingserver/ssh.png" height="100%" width="100%">



BUT OOPS , the “secretkey” need a password
The only feasible way forward is to crack the password using a password cracker like “JohnTheRipper” ,
but innocent john has no idea of that the KEY is and needs you to convert the file to what it can understand
so therefore we firstly need to convert the SSHKEY to what JohntheRipper understands using an inbuilt John plugin called SSH2JOHN
then we use John to crack the the file using the wordlist we recovered from the webserver

<img src="/assets/images/gamingserver/forjohn.png" height="100%" width="100%">


Now we have a Username, sshkey, and the password to the sshkey

<img src="/assets/images/gamingserver/login.png" height="100%" width="100%">

<img src="/assets/images/gamingserver/usertxt.png" height="100%" width="100%">

### PRIVILEGE ESCALATION
We use a method called **Lxd Privilege Escalation**
Privilege escalation through lxd requires the access of local account, 

Good thing for us since we have SSH access already

Note: the most important condition is that the user should be a member of lxd group.

If you have completed the introductory researching room on TryHackMe
Do your research on **LXD PRIVILEGE ESCALATION** and root the box


and remember 

>### The difference between a noob and a hacker is that a hacker has failed more than a noob has ever tried
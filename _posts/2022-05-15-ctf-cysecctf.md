---
layout: post
title: CYSEC 2020 CTF
categories: ctf
permalink: /:categories/cysecctf/
---

## **CYSEC CyberHackathon CTF**

## INTRODUCTION


<img src="/assets/images/cysecctf/intro.png" height="100%" width="100%">


Praticing competitive hacking helps build your quick analytical thinking and solidifies your methodology, Pwn2Own is a simple and intuitive machine from my buddy @rudeFish

_cysec.local_ being the domain name is a quick pointer of the machine being a domain joined AD object,

We kick off by adding the FQDN to the our PC's host file and  running a quick TCP scan 


```bash
sudo echo "cysec.local 54.234.92.201" >> /etc/hosts; \
nmap   -T4 -Pn --min-rate 1000 --open -r   54.234.92.201 
-oN Initial.Tcp -e wlan0  --top-ports 10000
```
<br>
<img src="/assets/images/cysecctf/nmapscan.png" height="100%" width="100%">

<br>
###Enumeration on port 21
FTP is immediately ignored :( a 5000 pointer shoudnt have anything to do port 21 🙄_justkidding_ 🙄
<br>
###Enumeration on port 80 
A quick enumeration on port 80 shows the default IIS webpage and fuzz of directories yield no result, 
<img src="/assets/images/cysecctf/iis.png" height="100%" width="100%">

looking at vhost/subdomain using FFUF
we find   `secret ` a to be a valid vhost 

<img src="/assets/images/cysecctf/vhostscan.png" height="100%" width="100%">
Adding the newly found vhost and the hosts file and fuzzing for subdirectories, we can find **`backups`** to be  valid 
```bash
sudo echo "54.234.92.201 secret.cysec.local " >> /etc/hosts; \
feroxbuster -u http://secret.cysec.local/
```
<img src="/assets/images/cysecctf/fericoxid.png" height="100%" width="100%">


Accessing the backups folder we can find a wordlist of usernames and passwords 
<img src="/assets/images/cysecctf/backups.png" height="100%" width="100%">
<br>
```bash
wget -q http://secret.cysec.local/backups/passwords.txt ;\
wget -q http://secret.cysec.local/backups/users.txt
```
<br>
Saving the wordlist and revoking our mental note about the existence of two other protocols : Lightweight Directory Access Protocol (LDAP) and the Server Message Block(SMB)
<br>
<img src="/assets/images/cysecctf/wget.png" height="100%" width="100%">


we proceed by  password spraying  both SMB and LDAP looking for valid credentials

### Enumeration on port 445
using CrackMapExec which is usefull in spraying passwords in a Active Directory network, we immediately get a hand of a valid
user credential `jsmith:password@123`
<img src="/assets/images/cysecctf/cme.gif" height="100%" width="100%">
<br>
### Exploiting SMB - 445
leveraging the credentials to list the available SMB shares 
<img src="/assets/images/cysecctf/smb1.png" height="100%" width="100%">


we can see see domain **$USERS** directory to which we can authenticate to, using the credentials we have 

<img src="/assets/images/cysecctf/smbclient.png" height="100%" width="100%">

Highlights for picture above
1. Authenticating to the SMB share.
2. Finding a powershell screipt containing credentials of another user
3. Downloading the script to our local machine.


The `read_appraisal_form.ps1` contains the hlevi domain user creds as we can see below
<img src="/assets/images/cysecctf/appraisal.png" height="100%" width="100%">

<br>
we proceed the exploitation process by leveraging the newly found creds to write and execute  to SMB share using evilwin-rm
<img src="/assets/images/cysecctf/winrm1.png" height="100%" width="100%">


<br>
looking at the list of users on the domain and enumerating each inidividually we can find the password of the user `hlevi` 
hidden in the comment field of the user property 

<img src="/assets/images/cysecctf/hlevi.png" height="100%" width="100%">


we can replicate the same SMB exploitation as earlier with the newly gathered  credentials 
<img src="/assets/images/cysecctf/winrm1.png" height="100%" width="100%">

<br>
this new user account is priviledged to read and write to the adminstrative share which give us access to the CTF flag!
<br>
<img src="/assets/images/cysecctf/flag.png" height="100%" width="100%">


All in all this was a simple, straight forward machine from stables of  `@rudefish`, 
pretty sure he would be dissapointed i solved this machine in user 12 minutes :) 🤣🤣
<br>

### Post Exploitaion
we proceed to the post exploition stage by first disabling the AV protection as well as Windows Defender Real Time Monitoring on the PC since we have administrative priviledges,
we use mimikatz to dump the hashes of other user on the machine to find lateral domain privilege escalation vectors.
<img src="/assets/images/cysecctf/disable.png" height="100%" width="100%">

<br>

also using PowerUp we can find numerous services that can be exploited to gain `SYSTEM` priviledges 
<img src="/assets/images/cysecctf/powerup.png" height="100%" width="100%">
<br>

we can aswell add our user to the administrator localgroup by abusing the vulnerable service
<img src="/assets/images/cysecctf/powerupex.png" height="100%" width="100%">
<br>
More windows persistence and clearing tracks should follow but thats definitely be yound the scope of this CTF. 
> **END OF PWN2OWN**



> **START OF REV**


<img src="/assets/images/cysecctf/intro.png" height="100%" width="100%">


We start of by loading the binary to GDB, setting our disassebly flavor to intel, we can as well use AT&T 
if we are much more conversant with the syntax
<img src="/assets/images/cysecctf/nofunctions.png" height="100%" width="100%">
<br>
we proceed by loading the functions of the binary with `load functions` which yields no funtion including `main` which is a wierd and usually a sign the binary has been packed with a packer.

as we dont know what kind of packer is in use, maybe a well known one or a custom packer we can string the binary for ascii content and grep 
for packer information
<img src="/assets/images/cysecctf/upxpacker.png" height="100%" width="100%">
<br>
we can find the packer used in this binary to be a well know packer `UPX`

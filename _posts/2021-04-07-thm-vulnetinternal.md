---
layout: post
title: "TryHackMe - VulnNetInternal"
categories: thm
permalink: /:categories/vulnetinternal/
---

# VulnNet: Internal TryHackeMe



Hello Guys. We would be attacking the VulnNet:Internal, Yet another amazing box from [TheCyb3rW0lf,](https://tryhackme.com/p/TheCyb3rW0lf) This machine test and sharpen’s your services enumeration skills

We start of my running a quick scan on all ports using threader300 and simultaneously running nmap service scan to cover the top ports
<br>
<img src="/assets/images/vulnetinternal/1*W8rhVtXIPg22Dl3XHzbEIw.png" height="100%" width="100%">

We immediately realize we need to enumerate several none http/https ports,
<br>
**SMB Enumeration : 138 | 445**

We we quickly list available share’s on the SMB server using the -L flag to list available shares and -N flag for a No Password login then immediately interacted with the “Vulnet Business Share” to get the Services Flag

<img src="/assets/images/vulnetinternal/1*1zSDALQTe1SsR9ijkdpBLw.png" height="100%" width="100%">
<br>
**RPC Enumeration : 111 ,**

We start by listing the share’s available to be mounted from the server using showmount, then we mount the share on out local machine in the /tmp/mnt directory

<img src="/assets/images/vulnetinternal/1*I5XyQHKecRKnmLIH4v_a2Q.png" height="100%" width="100%">

Enumerating the share, we quickly dive down to the Redis directory to find notable information in the redis.conf file

<img src="/assets/images/vulnetinternal/1*_9KJsriDvRGO4oRFHy_Ifg.png" height="100%" width="100%">*MasterPassword in redis.conf*
<br>
**REDIS Enumeration : 6379**

REDIS the Remote Dictionary Server is an in-memory database we could enumerate Redis with either Netcat, MSF auxiliary scanner or Redis-cli

using Redis-cli which the best in my opinion we connect to the Redis server using the credentials we found in the mount earlier then query it for the list and content of database it holds

<img src="/assets/images/vulnetinternal/1*zXg8DMiIxWHFyTwA7di1ug.png" height="100%" width="100%">

we found a notable rsync connection strings and The *INTERNAL FLAG* !,note it down and head back to the drawing board 
*Note Redis access could be used to gain Remote Code Execution using Crontab or placing SSH keys in any users $Home directory, none which worked in this instance
<br>
**RSYNC Enumeration : 873**

rsync is a utility for efficiently transferring and synchronizing files between computers, drives and networks

Checking for the available directory to be synchronized, we created a folder on our Local Working Directory then used rsyc to sync the remote folder to it

<img src="/assets/images/vulnetinternal/1*SEqxHETleWAtAWC4NarHJQ.png" height="100%" width="100%">

Navigating through the files, we find our *USER FLAG and the .SSH directory*
<br>
**GETTING A SHELL**

RSYNC has local and remote copy function’s, same way we were able to download the remote directory we could also put files in the remote directory

we immediately

* generate an SSH keypair ,

* place the public key in an authorized_keys files

* copy to the the authorized_keys to the remote .ssh folder after giving it correct chmod 600 permissions

After which we are able to SSH into the machine as “sys-internal”

<img src="/assets/images/vulnetinternal/1*C6-HbPhWF5rKF3y7GjPr4w.png" height="100%" width="100%">
<br>
**GETTING ROOT**

Enumerating for ports only accessible on the local network we find port 8111 to be running a web application “TEAMCITY”

<img src="/assets/images/vulnetinternal/1*cupzNaXhlXJGe3_eYpgQFw.png" height="100%" width="100%">

We forward this port to our machine using SSH port forward with the private key we created earlier

<img src="/assets/images/vulnetinternal/1*guzgkEZAD_n0n959FrFhJg.png" height="100%" width="100%">

<img src="/assets/images/vulnetinternal/1*XloBtB7JZyn5hBnJiFuTaQ.png" height="100%" width="100%">

Trying all credentials we found so far all to know avail we head back to the machine to search for more credentials and/maybe authentication token to login as a super user

Grepping for token, we find an authentication token that works in the password field without a username that in turn permits us to login into the “Teamcity” superuser dashboard

<img src="/assets/images/vulnetinternal/1*rkcby_NSSGskE6YjHwmlpA.png" height="100%" width="100%">
<br>
**GETTING ROOT Contd**

<img src="/assets/images/vulnetinternal/1*1iGV8uxlwhXNMz5KYSaMLQ.png" height="100%" width="100%">

Since TeamCity is running as root, whatever connection we can get it to spawn will be with root permissions, we immediately started to poke for console pages/terminal or anything that be used to run system commands

After a while we figured you can create a project then build configuration, skipping the question for “New VCS Root”,

<img src="/assets/images/vulnetinternal/1*uw6ntR_wrrZfrRy_LpwD3g.png" height="100%" width="100%">*Create a project*

<img src="/assets/images/vulnetinternal/1*OmimM9VbgHmibBs7Mw6qQQ.png" height="100%" width="100%">*Build Configuration*

After creating a build configuration 
choose “Build Steps” on the left menu to add a build step,

<img src="/assets/images/vulnetinternal/1*_nd5pRUxnZG1qf-xxUdsTw.png" height="100%" width="100%">

Choose the runner type “Python”. Choose command as custom script

then place a python3 reverse shell in the custom script section without the ‘python -c’ then run build in the upper left , definitely after setting up a listener

<img src="/assets/images/vulnetinternal/1*DyCYYloaZ2LtpG7R-tSamA.gif)

Root, Chill And Remember

### The difference between a noob and a hacker is that a hacker has failed more than a noob has ever tried :)


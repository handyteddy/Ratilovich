---
layout: post
title: "HackTheBox - Shibboleth"
categories: htb
permalink: /:categories/shibboleth/
---

#  WriteUp - HackTheBox

Shibboleth is a medium machine on HackTheBox that requires regular web application enumeration for user access and critical service version assessment for privilege escalation

biggest take away from this machine is the reminder to always look into services running on UDP

**Getting Into It**

As with other HTB machines we start off by adding the machines name to our /etc/hosts file and proceeding with a regular port scan to probe for open ports on the target

<img src="/assets/images/shibboleth/1eBTJDQruemZplse733JDIw.png" height="100%" width="100%">


futher UDP scan shows IPMI running on its regular port 623, Intelligent Platform Management Interface (IPMI) is a collection of specifications that define communication protocols for talking both across a local bus as well as the network.

<img src="/assets/images/shibboleth/1xrUMV-q8h7IhSIX7U8VGrw.png" height="100%" width="100%">

IPMI has a vulnerability which Basically,** allows you to request the server for the hashes MD5 and SHA1 of any username and if the username exists those hashes will be sent back.** And there is a **metasploit module **for testing this
> msf > use auxiliary/scanner/ipmi/ipmi_dumphashes

running the module againts the web server we are able to secure the hash of the the Administrator user

<img src="/assets/images/shibboleth/1-y-9_EdH6UEWpemmGM4cQA.png" height="100%" width="100%">

proceeding to crack the hash we recover a password for the Administrator account
> for those interested the hash format is “IPMI2 RAKP HMAC-SHA1” which is module 7300 on hashcat

<img src="/assets/images/shibboleth/1MxH7n3tx193M7wT7JlgODw.png" height="100%" width="100%">

without any further use of the IPMI protocol we proceed to enumerating TCP port 80

**PORT 80**

Enumerating port 80 shows a bootstrap HTML template running with no angle of exploitation

<img src="/assets/images/shibboleth/1_G1Q7m7FldBT-sOczCCbfA.png" height="100%" width="100%">

further check by way of subdomain enumeration reveals one web applications running on two different subdomains

“monitor” and “zabbix”

<img src="/assets/images/shibboleth/17eAU4863LtSgXQQ6jH_Hdw.png" height="100%" width="100%">

Looking at the subdomain we find Zabbix to be running, **Zabbix** is an open-source software tool to monitor IT infrastructure such as networks, servers, virtual machines, and cloud services.

<img src="/assets/images/shibboleth/1AhoLnOHcdibUntzhC1pTSw.png" height="100%" width="100%">
Though there is no way to figure the version of zabbix running, by reading the advisory on the zabbix official website we figure recent version of the zabbix web application to be vulnerable to an Authenticated Remote Code Execution Vulnerability

<img src="/assets/images/shibboleth/1HWF9n46q1vWM-j66V6SAbA.png" height="100%" width="100%">*Zabbix 5.0.17 — Remote Code Execution (RCE) (Authenticated)*

running the exploit against the target we secure a shell as the user Zabbix

<img src="/assets/images/shibboleth/1Yi9LrOUhR71vXAMkFP2OhA.png" height="100%" width="100%">

reading the **user.txt **file requires us to be privilege as the **ipmi-svc** user, we can do lateral privileged escalation to the **ipmi-svc** user by **“su ipmi-svc”** using the password earlier gathered from the IPMI vulnerability

<img src="/assets/images/shibboleth/1DUTeqOEF5Fbp3n0QJ2uIhQ.png" height="100%" width="100%">*user.txt*

**Horizontal Privileged Escalation**

By looking for credentials in configuration files

<img src="/assets/images/shibboleth/1t7tK5zt1sqol6VN6HjjiBg.png" height="100%" width="100%">*using find to enumerate conf files*

we are able to read clear text database credentials in the **zabbix_server.conf **file

<img src="/assets/images/shibboleth/1pW1zyqRlw-aK2Z6dcbsnIA.png" height="100%" width="100%">

authenticating to the MySql database with the credentials from the configuration file, we immediately notice the version of MySql to be a 10.3.25-MariaDB which is vulnerable to a code execution as **CVE:2021–27928**

<img src="/assets/images/shibboleth/1izbR30PUK0u_pTt0U5v3Pg.png" height="100%" width="100%">*service version enumeration*

exploiting the vulnerability require the attacker to create a reverse_shell binary preferable with **msfvenom** which is to be supplied to MySql as an executable using the -e parameter

<img src="/assets/images/shibboleth/1uV5W6MnEZ5okTWUNF2QzFA.png" height="100%" width="100%">*creating a elf binary with msfvenom*

we proceed the exploitation process by transferring the reverse shell payload to the target machine then connecting the MySql once again with the SET GLOBAL wsrep_provider variable set to our binary as illustrated in the PoC
> *PoC available at [https://packetstormsecurity.com/files/162177/MariaDB-10.2-Command-Execution.html](https://packetstormsecurity.com/files/162177/MariaDB-10.2-Command-Execution.html)

<img src="/assets/images/shibboleth/1jnQJobg2wJxSaJng3kKuwA.png" height="100%" width="100%">`mysql -u <user> -p -h <ip> -e 'SET GLOBAL wsrep_provider="/tmp/CVE-2021-27928.so";'`

Setting up a listener and running the exploit give us a a shell with root privileges as the MySql Service is running with root privileges

<img src="/assets/images/shibboleth/1*uCzDfgFX1UMSPL0SjNmlfA.png" height="100%" width="100%">

And as always, Remember

### The difference between a noob and a hacker is that, a hacker has failed more than a noob has ever tried

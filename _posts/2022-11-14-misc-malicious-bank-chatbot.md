---
layout: post
title:  "Rise in Malicious ChatBots - Bank Casestudy"
date:   2022-11-14 
categories: misc 
permalink: /:categories/maliciouschatbot/
---

# Rise in Malicious ChatBots - a UBA case study
## Part 1 - Introduction

<br>
Since the inception of web automation in the 2010s and the increasing need for customer retention through exceptional customer service, many companies have leveraged business features of social media networks to promptly address customer grievances and difficulties.

But with the adoption of new technologies comes the avenue for exploitation by threat actors. 
<br>
One very good business feature made available by instant messaging platforms like WhatsApp, Messenger, Telegram and Discord is ChatBots: which is a piece of automated messaging software that uses artificial intelligence to converse with customers
Threat actors have indeed weaponized this feature for use in phishing campaigns and sometimes for Command and Control purposes. 
<br>
In this article we will drill in on a somewhat advanced campaign where threat actoors are masquerading as a renowned bank in Africa, UBA and harvesting debit card information as well as its corresponding 2FA 

As an average bank account owner with some banking difficulties, going on to Messenger with the intention of seeking customer service, you may come across two or more ChatBots depending who or what is being impersonated.
<br>
<img src="/assets/images/bankchatbot/1.jpg" height="80%" width="70%">
<br>
Interacting with the first Chatbot proved abortive as the agents are busy but a second identical Chatbot offers to resolve your issues by asking you to “Follow A Link” in order to attend to your request.

 <img src="/assets/images/bankchatbot/1s.png" height="50%" width="70%">
<br>
Upon following the link we are greeted with a "not so obvious" phish page requesting for:
• Account Number
• Card Number
• Expiration Date
• CVV
• PIN
<br>
 <img src="/assets/images/bankchatbot/mainpage.png" height="100%" width="100%">

Traditonally the compromise of the above information wouldn't be a problem as the malicious subject cannot get the bank to authorise transactions by merely supplying just the card details.
Credit and debit card issuers now have additional layers of authentication for approval of transations - **Visa** has **Verified By Visa**, **Mastercard** has **SecureCode By Mastercard**. Nigerian banks also have The **OTP (One Time Password)**, which is a private code or unique password that gives you added protection against unauthorized use of your card when making payments or shopping online. 
 <br>
To get around this layer of authentication, the actors have *man-in-the-middled* the campaign by also requesting for the users OTP, and then using that OTP to validate transactions.
 <br>
 <img src="/assets/images/bankchatbot/otppage.png" height="100%" width="100%">

If you wonder how they can achieve this in real time... **Read Further**.
 
After submission of a One Time Password we are greeted with a success page [[more like  good luck your account has been emptied LOL]]

<img src="/assets/images/bankchatbot/completed.png" height="100%" width="100%">
<br>

## Part 2 - Some Technical Analysis

Now to the fun part. As the jobless hacker that i am 😊, I initiated the weapon of mass destruction: My brain, attacked the web application and got into the server. 
It was quite dissapointing to realize the web application makes use of shared hosting but nevertheless the privilege gave me access to the campaign materials and data which enable us see how the campaign operates.
<br>
For the sake brevity, I will be skipping certain pages and only focusing on the ones with key functions.
 <br>
First, we get to see how successful this campaign has been with some card details and their corresponding OTPs
<img src="/assets/images/bankchatbot/logs.png" height="70%" width="70%">
 <br>

The index page calls **login.php** and generates a random md5 string for use as a session identifier.
 <img src="/assets/images/bankchatbot/indexsource.png" height="100%" width="100%">
 <br>
In login.php, we are only concerned with the form action which helps us determine where the posted data is being sent to. In this case as we will see below, **Mail1.php** handles the supplied data.
<img src="/assets/images/bankchatbot/loginsource.png" height="100%" width="100%">
 <br>
Traditional phishing kits send harvested data to an email address using the phpmailer function. However looking at **Mail1.php** this kits leverages Telegram's ChatBots API to instantenously notify the attacker of a new submission - which includes debit card data and OTP information.
<img src="/assets/images/bankchatbot/mail1source.png" height="75%" width="75%">
 
1. Telegrams API endpoint
2. Parameter supplies to the endpoint
3. Harvested data sent along with the post request
4. The OTP page in which the victim would be redirected to for harvesting the authenication codes
 <br>
 
Looking at the OTP/email verification page, we can see the form action to be mail2.php
<img src="/assets/images/bankchatbot/otpsource.png" height="100%" width="100%">
 <br>
Mail2.php is identical to mail1.php. as its send the supplied OTP to the attacker's telegram group in real time
  <img src="/assets/images/bankchatbot/mail2source.png" height="75%" width="75%">

1. Ability to send data to Telegram or Discord
2. After OTP submisson you get redirected to a prof.php page
<br>
Prof.php is the success page that stays up for a 3.5 seconds before redirecting to the legitmate url for the UBA
 
 <img src="/assets/images/bankchatbot/profsource.png" height="100%" width="100%">
 <br>
 
Some other features of this kit are as below
<img src="/assets/images/bankchatbot/antidetect.png" height="100%" width="100%">

 1. The **blacklist** reads several IP's of a bot.txt text file  and block access for those address
 2. The **Bot-Crawler** continully harvest address of known bots and append the to the bot.txt file
 3. **Bot-Spox** is quite interesting as its harvest new bots as well
 4. **Dila_DZ** Perform a HTTP REFERER check on the visitor to see if they are coming from the Phishtank website
 5. **IP-Blacklist** blocks access for hardcoded IP ranges
 
<br>
And the interesting stuff never ends
 
<img src="/assets/images/bankchatbot/antidetect2.png" height="100%" width="100%">

1. Checks the validity of the card you supplied by looking up the BIN in a bin database
2. Checks the Operating System the supplier uses and determine if its blockworthy or not [FU.php lol]
<br>
<br>
I was also able to get the telegram bots token and chat ID which could be used to social engineer the actor and maybe figure those behind 

<img src="/assets/images/bankchatbot/tokensource.png" height="100%" width="100%">
 <br>
 
but like cybersecurity folks like to say “You need permission, bla bla bla, yada yada yada”. 🤦  🤦  

 
Now you might wonder how the attacker makes money from all this, they may use your card in real time and link to services like Quickteller, OPay, Jumia, Aliexpress etc, verify with your supplied OTP, then use such accounts for bill payments, purchases and/or withdrawals.
 
## Part 3 - Countermeasure
 <br>
Technically this success of this campaign and similars ones is in no way the fault of the company being impersonated in this case **UBA**, as it is a bank well known for its strong cybersecurity posture nevertheless a lot of research need to be done in the field of authentication and payment processing by the cybersecurity community, OTP are facing out as there are TOTP, HOTP and authentications like FaceID, payment authetications like PayConfirm and so on.

But as always the best line of defence against phishing is awareness and training hence the need for more articles like this one.

<br>

> **Opinions here are my own and not the views of my employer**
<br>
> **Open to any work that'll make the CISO ~~loose thier job~~ happy 😀  ~~in other words VA/PT/RT~~
<br>
> **Resume at : [Online Resume](https://www.redteam.ng/resume)**

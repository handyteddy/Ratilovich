---
layout: post
title:  "How To Protect Your Privacy On Android"
date:   2017-03-12 
categories: android privacy
---
## How To Protect Your Privacy On Android
I was recently [shown an interesting blog post by the DuckDuckGo team](https://spreadprivacy.com/iphone-privacy-tips/#.5vdr8rnbg) showing how an iPhone user could go about protecting their privacy making various changes to the phone. In an effort to help Android users become more aware of how they can protect their privacy as well, I thought I would compare privacy options for iOS and Android, as well as show some other ways Android users can protect their privacy. The first 11 steps will directly contrast the steps shown in the DuckDuckGo article.

<br>
## 1. Use a custom passcode longer than 4 digits.

If you haven’t yet set up a password on your Android device, it’s always a good time to do so. In addition to protecting your information from being accessed from the device itself, applications that request sensitive permissions from the device will the device to prompt you for the password to be entered as well to ensure that it’s actually you giving the app permission to your info.

### Instructions: Settings > Security > Screen lock (location may vary depending on Android version/manufacturer) > Password

Note that this password is independent of your Google password. You are presented with other options as well, such as a pattern or PIN. Passwords are the most secure option; [patterns](http://www.makeuseof.com/tag/pattern-locks-not-secure-android-devices/) and [PINs](https://www.hak5.org/episodes/hak5-1217) can often be cracked within hours, if not minutes.

<br>
## 2. Enable “Erase Data” to delete data after 10 failed passcode attempts. (Bonus: encrypt all of your storage, including the SD card)

A major issue with wiping data is that doing so requires it to be overwritten, not simply “deleted”. This can take hours, if not days, to do thoroughly on devices with flash memory (like smartphones). If an Android device were to attempt to wipe itself like this after being bruteforced, the attacker would have an opportunity to try to retrieve the information again.

The solution implemented by the Android developers is to allow the user to encrypt the data on both the internal and external SD card (since Android devices have those), that way if the password is entered too many incorrect times, the significantly smaller encryption key is wiped instead, rendering the encrypted information useless.

### Instructions:

* If you’re on Android 7.0 or later, your device already does this by default, as long as you have a screen lock enabled, as described in the prior step. Congratulations! You can read more about it [here](https://source.android.com/security/encryption/file-based.html).
* If you’re on Android 6.0.1 or earlier, you’ll first want to enable a screen lock, which can be done with the prior step.
* Next, you’ll want to head to Settings > Security, and select the option to encrypt your device. It should say something along the lines of “Encrypt phone” and/or “Encrypt SD card storage”. You can choose which you want to do. Be careful though: if you encrypt your SD card and reset your phone, sell it, trade it in, etc., your SD card will be inaccessible because the data are still encrypted with the old encryption key!

Note: you can see what version of Android you have by following this [quick guide](https://support.google.com/pixelphone/answer/4457705). It was written for the Google Pixel, but should work for most Android devices.

<br>
## 3. Don’t show notifications in the lock screen for sensitive apps.

Before Android 5.0, no notifications were shown on the lock screen whatsoever. After 5.0, though, users were given the choice of seeing notifications on the lock screen in their entirety, seeing the application but hiding the contents, or not showing anything, as was the case in previous versions of Android.

### Instructions:

* As with Step 2, you’ll first want to enable a screen lock on your device.
* After that, go to Settings > Sound & Notification. At this point, you’ll be able to choose between “Show all notification content,” “Hide sensitive notification content,” and “Don’t show notifications at all”.
* If you choose the second option, you also get to choose which of your apps are considered sensitive! All are by default, but if there’s an app whose information you do want visible on the lock screen, you can go to Settings > Apps > [An app of your choosing] > Notifications, and you can choose your desired settings.


<br>
## 4. Turn off “Share My Location.”

This is a feature exclusive to iOS devices. Android does not inherently share your location with family and friends. Some apps that you may have installed, such as Google+, may do so, but that can be easily disabled if you… 

<br>
## 5. Turn off location services for things that don’t need them.

In the Android 4.0 beta, a hidden feature known as “AppOps” was present, which allowed users to disable certain permissions of a particular app. For reasons unknown, this was removed in the release version of 4.0, but it has been implemented as an app by third-party developers. One such example can be found [here](https://play.google.com/store/apps/details?id=com.findsdk.apppermission&hl=en). If you have Android 4.3-5.1, this app will allow you to disable location services on an app-by-app basis.

### Instructions:

* If you have a version of Android including or after 4.3 and before 5.1, use [AppOps on the Google Play Store](https://play.google.com/store/apps/details?id=com.findsdk.apppermission&hl=en) to disable location settings for individual apps
* If you have Android 6.0 or later, you can do this without a third-party app, as the functionality was returned as an official feature with the release of 6.0. Though the specifics may vary from device to device, the general idea is to go to Settings > Apps > Permissions > [An app of your choosing] > Permissions > Whatever permissions you want to disable – “Location” in this particular case

Note: If you want a list of apps that have requested your location in the past as a reference, you can go to Settings > Location, where you should see a list of apps that have made these requests.

<br>
## 6. Turn off access to sensitive data for apps that don’t need it.

The instructions from step 5 can be used to restrict access to private information if you have an Android device on version 4.3 or later.

<br>
## 7. Review your installed apps.

It never hurts to go through your installed apps once in a while and uninstall the ones you don’t use. There’s a chance the app may be draining your battery in the background, or could be a potential vulnerability if it’s not by an established developer (or sometimes, even [if it is](https://www.techworm.net/2016/06/hackers-hack-facebook-messenger-app-read-alter-messages.html))

### Instructions:

* Settings > Apps > [An app of your choosing] > Uninstall


<br>
## 8. Turn off read receipts so people are not notified when you see their messages.

Android has supported disabling read receipts for as long as they’ve been a part of Android (which hasn’t been too long to begin with).

### Instructions:

Though the particular steps once again vary depending on your version of Android and the manufacturer of your device, this is the general idea of where you want to go:

* Messaging app > Menu (may be shown as three dots) > Settings > Messages/Text Messages/Multimedia Messages (may be under “advanced”, “more”, etc.) > Allow read reports/Allow delivery reports


<br>
## 9. Turn on “Limit ad tracking”.

Android advertising is done through Google Ads, and can be limited through the Google app

### Instructions:

Settings > Google services > Ads > Opt out of Ads Personalization

<br>
## 10. From time-to-time, reset your advertising identifier.

As with the previous step, this can be done with with the Google app, under the same menu.

Instructions

Settings > Google services > Ads > Reset advertising ID > Confirm

<br>
## 11. Set DuckDuckGo as your default search engine.

Given that this was a post originally on the DuckDuckGo blog, one could expect a plug for using DuckDuckGo as your search engine. The steps vary depending on your browser, but specific instructions can be found on the [DuckDuckGo Android Support Page](https://duck.co/help/mobile/android).

<br>
## Bonus: Set up Android Device Manager

Android Device Manager is an entirely free service by Google that allows you to remotely lock, ring, or wipe your device. The steps to ensure that it’s working properly can be found on [Google’s official Android Device Manager support page](https://support.google.com/accounts/answer/3265955?hl=en).

<br>
## Bonus: Block ads and trackers

If you have Firefox installed on your Android device (my personal Android web browser recommendation as a result of being publicly licensed and open-source), you can install the [uBlock Origin add-on for Firefox for Android](https://addons.mozilla.org/en-us/android/addon/ublock-origin/). Navigate to that page on your device and press “Add to Firefox”. uBlock Origin will automatically begin blocking ads and trackers that appear in your visited sites.

<br>
## Bonus: Avoid Malware

One of Android’s greatest strengths are also one of its greatest weaknesses… as far as security goes, anyway. Android is more open than iOS in many ways, one of which being that users are able to install their own applications, whereas all iOS applications must be installed through the app store.

When installing an app, regardless of where it originates (but especially if it’s not through the Play Store), be sure that you trust the source of the app. Google doesn’t have any control over apps outside of the app store, so it doesn’t pass Google’s anti-malware guidelines before it makes it to your device. Fortunately, on Android, malware is rare outside of rogue apps, so as long as you’re installing trusted apps, you should be fine.

# DLink Cameras DCS-934L Setup and Settings access to configure motion detection and setup notification emails

## Connect DCS-934L camera to router

- Using MyDlink Light smartphone app.
  - Setup camera from scratch
  - It will require connecting camera to the Wifi router using WPS buttons.
  - If the Wifi router Access Point is hidden, WPS will not work --> disable Hidden network first on the router.
  - Connect Camera to Wifi router using WPS.
  - Then Camera is setup on the Wifi network and configured in the Smartphone MyDlink light app.
 
## Setup Camera email notifications using Windows / Internet Explorer / Camera html page

- D-Link does not support anymore those obsolete cameras, therefore login into the www.mydlink.com will indicate we need to use an obsolete Internet Explorer browser or an very old specific Firefox browser version to be able to connect to the camera.

- The URL www.mdlink.com, after login, will lead to this page: https://www.mydlink.com/device/unsupport_os_browser
```
Unsupported Browser or Operating System Detected!

You are using an unsupported browser or operating system and therefore the mydlink web portal may not look, behave or function as intended.

What operating systems and browsers does mydlink support?

We recommend you use Firefox 12-51/52 ESR on Windows or MacOS to access the mydlink portal. Alternatively, you can use our mobile apps to access your devices

Check out mydlink mobile apps.
```

- One workaround is to use Microsoft Edge browser, enable the "Internet Explorer compatibility".
```
Make legacy sites work in Microsoft Edge

Are you facing issues in opening legacy sites? With Internet Explorer mode, you can open legacy sites in Microsoft Edge. Select Add under Internet Explorer mode pages to add any legacy site to list of sites that will open automatically in Internet Explorer mode.

Allow sites to be reloaded in Internet Explorer mode (IE mode)  ---> TO BE SET TO "Allow".
When browsing in Microsoft Edge, if a site requires Internet Explorer for compatibility, you can choose to reload it in Internet Explorer mode

Internet Explorer mode pages --> WE CAN ADD URLs we want Edge to open with Internet Explorer Compatibility Mode.

These pages will open in Internet Explorer mode for 30 days from the date you add the page. You have 3 pages that'll automatically open in Internet Explorer mode.

https://mydlink.com/
https://www.mydlink.com/device/unsupport_os_browser
```
- Edge will show an icon on the top right corner, representing Internet Explorer Logo, to switch to "Reload tab in Internet Explorer Mode".
- To this effect, via Microsoft Edge browser, use the DCS-934L IP address as URL to open the camera html settings webpage.

## Gmail configuration for motion detection email notifications

- Setup SMTP server address and port as recommended from Gmail.
- For Gmail account and password, Gmail does not allow anymore to use directly the Gmail password, so we need to go to the Gmail/Google account / Security. And then, "Enable 2-step verification on your Google account, then generate an App Password to use with the camera.  Use smtp.gmail.com, port 465/SSL or port 587/STARTTLS, your Gmail address as username and the App Password."

## Next project: build an old Ubuntu Docker image with and old Firefox version (12-51/52 ESR)

Preliminary infos for this: 

Firefox 12-51/52 ESR      

2000, XP RTM–SP1 and
Server 2003 RTM	10.0.12esr	2004–2013
12.0	2004–2012

XP SP2+, Server 2003 SP1+ & R2,
Vista and Server 2008				52.9.0esr (IA-32)	2004–2018
									52.0.2 (IA-32)	2004–2017

									Linux

Firefox 96 on Arch Linux
Opening Wikipedia main page with Mozilla Firefox 99 on Ubuntu 20.04
Since its inception, Firefox for Linux supported the 32-bit memory architecture of the IA-32 instruction set. 64-bit builds were introduced in the 4.0 release.[180] The 46.0 release replaced GTK 2.18 with 3.4 as a system requirement on Linux and other systems running X.Org.[192] Starting with 53.0, the 32-bit builds require the SSE2 instruction set. Firefox also can run on number of other architectures on Linux, including ARM, AArch64, POWER/PowerPC/Power ISA, SPARC, PA-RISC, MIPS, s390, and in the past Alpha, IA-64 (Intel Itanium) and m68k.

2010, Ubuntu 10.04


Ubuntu 11.04 (Natty Narwhal) 

Ubuntu 11.04 Desktop (Natty Narwhal) using Unity
The naming of Ubuntu 11.04 (Natty Narwhal) was announced on 17 August 2010 by Mark Shuttleworth.[102] Ubuntu 11.04 Natty Narwhal was released on 28 April 2011.[103] It is Canonical's 14th release of Ubuntu. Support ended on 28 October 2012.[104] Ubuntu 11.04 used the Unity user interface instead of GNOME 2 as default. The move to Unity was controversial as some GNOME developers feared it would fracture the community and marginalize GNOME Shell.[105][106] Ubuntu 11.04 employed Banshee as the default music player, replacing Rhythmbox. Other new applications included OpenStack,[107] Firefox 4,[108] and LibreOffice, which replaced OpenOffice.org.[109] The Ubuntu Netbook Edition was merged into the desktop edition.[110] Jesse Smith of DistroWatch criticized the instability of the release. [111]

https://stackoverflow.com/questions/20414036/run-old-linux-release-in-a-docker-container

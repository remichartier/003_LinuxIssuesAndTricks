# Linux / Windows 10 Dual Boot : How to directly reboot from Windows to Ubuntu independently of the primary boot OS

Source : Method 3 out of 4, from this article : https://www.intowindows.com/4-ways-to-change-the-boot-order-in-windows-10/

- From Windows 10 : 
  - Settings
  - Update & Security
  - Recovery
  - Advanced Startup
  - Restart Now
  - Choose Options
  - Use a device

Then select the OS you would like to boot on (Ubuntu for instance).
It will boot on Ubuntu even if Priority boot was Windows.

This is useful if controling the computer remotely and not being physically local to the computer to switch boot manually from Windows to Ubuntu.

Note : 
- I noticed that if accessing the computer remotely via Remote Desktop Sharing, the option "Advanced Startup" may not be available sometimes, possibly due to some access right issues when logged remotely.


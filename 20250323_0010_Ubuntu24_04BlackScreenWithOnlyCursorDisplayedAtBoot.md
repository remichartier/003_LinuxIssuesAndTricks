# Ubuntu 24.04 Black Screen With Only Cursor Displayed At Boot
## Sources
- https://askubuntu.com/questions/1514757/issue-with-ubuntu-24-04-black-screen-with-cursor-on-login
- https://bugs.launchpad.net/ubuntu/+source/gnome-shell/+bug/2089709?comments=all

Graphic manager used by default on Ubuntu 24.04: gdm3.
For the time being, the only way I could work around this issue:
```
Ctrl+Alt+F4 allows to switch to a terminal (Ctrl+Alt+F7 to switch back to Graphic manager display)

sudo apt update
sudo apt install lightdm

During the installation, you might be prompted to choose the default display manager. If not, you can manually reconfigure it:

sudo dpkg-reconfigure lightdm

You will be presented with a dialog to choose the default display manager. Select lightdm or gdm3 as per your preference.

I selected lightdm to workaround this issue temporarily until it gets fixed with gdm3.

Restart your system:

sudo reboot
```
No other solutions mentioned in the sources worked for me so far.
To be able to switch back to gdm3 login again, I found out that in the file "/etc/gdm3/custom.conf", the "WaylandEnable" line was commented. I have no idea why, because I never modified this file before:

```
# Uncomment the line below to force the login screen to use Xorg
#WaylandEnable=false
```
After uncommenting this line, and rebooting with gdm3, I landed again on the login window as expected.

I also noticed that when I was trying to login via gdm3, using Wayland instead of X11 (WaylandEnable=true), then I would fall back on the same initial issue, no login screen, just a black screen with a mouse cursor. Essentially same failure as if I had that commented line "#WaylandEnable=false".

I suspect that one of the latest Ubuntu update forced to use Wayland instead of X11 for the login screen, by commenting the line "#WaylandEnable=false". And apparently, Wayland login would fail to launch on my system.

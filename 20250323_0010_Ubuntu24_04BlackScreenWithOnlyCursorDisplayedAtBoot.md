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

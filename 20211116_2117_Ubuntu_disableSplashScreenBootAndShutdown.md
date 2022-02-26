# Linux Ubuntu : Disable splash screen at boot and shutdown

- Edit `/etc/default/grub`

- And remove the "quiet splash" from the Linux command line:

- Here's what it looks like by default:

```
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"
```
- Make it look like this:

```
GRUB_CMDLINE_LINUX_DEFAULT=""
```
- After this run :

`sudo update-grub`


## Sources : 

[1] : [How do I disable the boot splash screen, and only show kernel and boot text instead?](https://askubuntu.com/questions/33416/how-do-i-disable-the-boot-splash-screen-and-only-show-kernel-and-boot-text-inst)

# Modifying Boot background image : 

- One example here : https://ubuntuhandbook.org/index.php/2020/05/login-screen-background-ubuntu-20-04/#:~:text=Besides%20typing%20the%20path%20to,it%20asks%20and%20hit%20Enter.
- Also : https://askubuntu.com/questions/1227070/how-do-i-change-login-screen-theme-or-background-in-ubuntu-20-04

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

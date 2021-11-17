# Ubuntu 20.04 : Enable Hibernate on Lenove Ideapad 3i Gaming laptop

## Configure properly swapfile size

According to [1] : 

> "Hibernate saves all of your RAM data on the hard disk and restores back into RAM after you turn on the computer."
.....
> "That’s why the swap partition must be more than or equal to RAM. To check your swap partition open ‘System Monitor’."

> "In the Resources Tab check your RAM and Swap. If swap is more than RAM, you’re good to go"


According to [2] : 

In order to do so, you must first disable the current swap space.

This action may take a minute or so to execute, so don’t panic!

`sudo swapoff -a`

You can now resize the swap space with fallocate. In this example, I am increasing it to 2GB. (But on my on laptop, needed to increase to 8G, equivalent to RAM size)

`sudo fallocate -l 2G /swapfile`

Now check how much swap space is configured with:

`ls -lh /swapfile`

Output:

`-rw------- 1 root root 2.0G Feb 13 03:12 /swapfile`

Above we can see there is now 2GB of swap space configured.

Make the swap file only accessible to root.

`sudo chmod 600 /swapfile`

Mark the file as a swap file.

`sudo mkswap /swapfile`

You may see a warning when resizing a previous swap file.
```
mkswap: /swapfile: warning: wiping old swap signature.
Setting up swapspace version 1, size = 2 GiB (2147479552 bytes)
no label, UUID=db0ee16f-a97f-4df0-a83e-713cd874a3fe
```
Finally we will tell the system to start using our new swap file.

`sudo swapon /swapfile`

To verify that the swap is now available, type:

`sudo swapon --show`


Output:
```
NAME      TYPE SIZE  USED PRIO
/swapfile file   2G 35.3M   -2
```
Above we can see a 2GB swap file available.

We can also run the following command to see our new swap file alongside physical memory.

`free -h`
```
              total        used        free      shared  buff/cache   available
Mem:           985M        674M         66M         61M        244M        110M
Swap:          2.0G         77M        1.9G
```
Your resized swap is ready to go!

If you can, reboot the server with sudo reboot and run sudo swapon --show again just to make sure the swap space was created automatically on startup.


## Enable Hibernate on Swap File and Resume on Swap file via Kernel parameter

According to [3] :

Find the UUID & Offset:
Since the file is created on Ubuntu file-system. It can be located via root UUID as well as physical offset.

To see your Ubuntu partition, run command and find the one mounted on ‘/‘:

`df -h`

Then find its UUID via command:

`blkid`

In my case, it’s ‘/dev/sda5’ and UUID is marked in white background.

To find the physical offset for /swapfile, run command:

`sudo filefrag -v /swapfile`

Copy the start number under physical_offset. It’s 927744 in my case.

Note : There is an easier way proposed by [4] : 
- Find your UUID and swap offset:

  - `findmnt -no UUID -T /swapfile && sudo swap-offset /swapfile`

- You will see something like this:

    ```
    371b1a95-d91b-49f8-aa4a-da51cbf780b2
    resume offset = 23888916
    ```
Finally edit the Grub configuration file (or use Grub-Customizer) via command:

`sudo gedit /etc/default/grub`

Then add `resume=UUID=xxx resume_offset=xxx` as value of “GRUB_CMDLINE_LINUX_DEFAULT”. Also replace ‘xxx’ with the id and/or offset value.

Exemple : `GRUB_CMDLINE_LINUX_DEFAULT="quiet splash resume=UUID=371b1a95-d91b-49f8-aa4a-da51cbf780b2 resume_offset=23888916"`

And update grub to apply change via command:

`sudo update-grub`

## Download hibernate package

According to [4] and also other references  : 

Install pm-utils and hibernate:

`sudo apt install pm-utils hibernate`

Then:

`cat /sys/power/state`

You should see:

`freeze mem disk`

Test hibernate : `sudo hibernate`

## Problem : `Failed to hibernate system via logind: Sleep verb not supported`

cf [5], this seems to be due to Secure Boot activated in BIOS/UEFI settings.

`It seems that hibernating doesn't really work with Secure Boot.
....
Shame the message did not read: Failed to hibernate system via logind: Please use BIOS to disable secure boot `


"I was finally able to solve my own problem following some topics on Fedora (they made the switch to systemd a while ago so there's more material there).

It turns out that I had secure boot enabled (I recall being asked about that during 16.04 install, and that I kept it on without giving it much thought) and that caused the output of cat /sys/power/disk to be:"

```
 [disabled]
```

"Indeed not a very good sign. So I rebooted and went searching in my BIOS settings, disabled secure boot there. Now cat /sys/power/disk gets me:"

```
 [platform] shutdown reboot suspend 
```
which looks better. 

[6] explains what is Secure Boot on PCs, and for Linux it seems ok or rather safe to disable it in BIOS/UEFI settings.


## Problem : Tuxonice and nvidia_drm, nvidia_modeset, nvidia

`sudo hibernate`

gives : 

```
hibernate:Warning: Tuxonice binary signature file not found.
Some modules failed to unload: nvidia_drm nvidia_modeset nvidia
hibernate: Aborting suspend due to errors in ModulesUnloadBlacklist (use --force to override).
```

cf [7] :

- `hibernate won't work with Nvidia's On-demand prime profile, but works with Performance or Intel profile`

--> Using `NVidia X Server Settings` App, I switched GPU mode from `Performance` to `Intel (Power Saving Mode)`, then the 'sudo hibernate' and resume worked successfully.

cf [8] :

For `hibernate:Warning: Tuxonice binary signature file not found.`, it is not blocking the hibernate, and I could not find any litterature online on how to fix this warning.


## Sources : 

[1] : [How to Enable Hibernate in Ubuntu Linux](https://www.linuxandubuntu.com/home/how-to-enable-hibernate-in-ubuntu-linux)
- Explain need for swap file or swap partition to be properly sized.

[2] : [How To Create or Resize Swap Space on Ubuntu 20.04 – 20.10 & 18.04 – 19.10](https://devanswers.co/creating-swap-space-ubuntu-18-04/)
- Paragraph `Increase or Resize Swap Space`

[3] : [How to Enable Hibernate Function & Menu Option in Ubuntu 21.10](https://ubuntuhandbook.org/index.php/2021/08/enable-hibernate-ubuntu-21-10/)
- Paragraph `Enable Hibernate on Swap File`

[4] : [How to enable the hibernate option in Ubuntu 20.04?](https://askubuntu.com/questions/1240123/how-to-enable-the-hibernate-option-in-ubuntu-20-04)
- intall pm-utils and hibernate packages

[5] : [How to activate hibernation in 16.04.1 ? (systemd)](https://askubuntu.com/questions/868208/how-to-activate-hibernation-in-16-04-1-systemd)
- This page infers that `Failed to hibernate system via logind: Sleep verb not supported` is due to Secure Boot activated in BIOS/UEFI settings.

[6] : [Disabling Secure Boot](https://docs.microsoft.com/en-us/windows-hardware/manufacture/desktop/disabling-secure-boot?view=windows-11) 
- Explanation of Secure Boot, it seems ok and reasonable to disable it on BIOS/UEFI for Linux laptops.

[7] : [I am having problem with hibernate. I have ubuntu 20.04LTS and it doesn't hibernates](https://stackoverflow.com/questions/63572394/i-am-having-problem-with-hibernate-i-have-ubuntu-20-04lts-and-it-doesnt-hibern)
- Nvidia mode blocking hibernate functionality

[8] : [hibernate:Warning: Tuxonice binary signature file not found](https://askubuntu.com/questions/1062206/hibernatewarning-tuxonice-binary-signature-file-not-found)
- No fix for this no blocking warning on Tuxonice

[9] : [Ubuntu 18.04 can't resume after hibernate](https://askubuntu.com/questions/1034185/ubuntu-18-04-cant-resume-after-hibernate/1064114#1064114)
- Additional info about swap files and activating hibernate feature on Linux Ubuntu
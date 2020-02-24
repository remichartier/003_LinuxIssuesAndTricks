HP Pavilion DV6 AMD Fan Always Running

# My problem : 
* HP Pavilion DV6 US version (AMD with AMD/ATI GPU) laptop Fan always running at maximum after a while.
* Using Lubuntu 18.04 (Light Ubuntu).

# General solution :  

Try setting both the CPU and GPU power/frequency profiles to low and see if it helps.

This paper only covers my efforts to set the GPU power/frequency profiles to the lowest possible in an attempt to reduce drastically the fan speed and noise of my HP Pavilion DV6 AMD laptop.

# My GPU configuration : 

`"lspci | grep VGA” `

gives : 

`01:05.0 VGA compatible controller: Advanced Micro Devices, Inc. [AMD/ATI] RS880M [Mobility Radeon HD 4225/4250]`

Using open source AMD/ATI Radeon video driver provided by Linux.

According to some comments seen on forums, this open-source Radeon driver is not good with power management on laptops (--> fan always running full speed). [1]

# What I found through my investigations and research :

* Even when setting CPU mode is set to “powersave” via different tools, Fan is always noisy and running at max speed after a while.
* This could be due as well to the GPU being configured at maximum performance by (L)Unbuntu 18.04 and therefore warming up so much that the Fan need to run at maximum speed.
* The biggest issue is that Lubuntu 18.04 sets the power profiles always to high on this configuration by default, making the CPU/GPU running highest voltage/highest frequency so that the fan is always forced to be at maximum speed and noise to try to cool down the CPU/GPU unit, not using any dynamic power management control.

# Background and Info retrieved from different sites/forums discussions about GPU power management settings : 

For this kind of GPU [AMD/ATI] RS880M [Mobility Radeon HD 4225/4250], Linux provides free Radeon drivers using “KMS”.

The other alternative would be to use proprietary drivers from AMD/ATI, so called Fglrx / Catalyst legacy drivers (RIP). 
* However those drivers are only working / compatible with older versions of Linux Kernel, used previously up to Ubuntu 12.04. 

And so nowadays for older AMD/ATI GPU processors like Radeo HD 4225/4250, the only solution available is the free open source driver from Linux mentioned above. 

And according to some comments I’ve seen on forums, this driver works great but is not good for managing Power Management and Fan speed, contrarily to the previous AMD/ATI proprietary drivers.

## Extracts from [2] and [5] :

KMS Power Management Options.
KMS = Kernel Mode Setting. Method for setting display resolution and depth in the kernel space rather than user space.
Kernel 2.6.35 or newer is required. 

The pm code supports three basic methods:
1. "dynpm"
1. "profile"
1. "dpm"

Ways to select the different power management methods are detailed later below in this document.

Note :  "dpm" support is only supported on R6xx and newer asics.

Controlling the fan speed directly is not possible (and would be very dangerous), but it can be lowered by setting lower power profile.

### The "dynpm" method = Dynamic frequency switching (Old method). 

This method dynamically changes the frequency depending on GPU load,dynamically changes the clocks based on the number of pending fences, so performance is ramped up when running GPU intensive apps, and ramped down when the GPU is idle. The reclocking is attemped during vertical blanking periods, but due to the timing of the reclocking functions, doesn't not always complete in the blanking period, which can lead to flicker in the display. Due to this, dynpm only works when a single head is active.

### The “profile” method : Profile-based frequency switching

This method will allow you to select one of the five profiles (described below). Different profiles, for the most part, end up changing the frequency/voltage of the GPU. This method is not as aggressive, but is more stable and flicker free and works with multiple heads active.

The "profile" method exposes five profiles that can be selected from:
1. "default"
1. "auto"
1. "low"
1. "mid"
1. "high"

More details about each profile : 

1. "default" uses the default clocks and does not change the power state. This is the default behavior.
1. "auto" selects between "mid" and "high" power states based on whether the system is on battery power or not. The "low" power state are selected when the monitors are in the dpms off state.
1. "low" forces the gpu to be in the low power state all the time. Note that "low" can cause display problems on some laptops; this is why auto does not use "low" when displays are active.
1. "mid" forces the gpu to be in the "mid" power state all the time. The "low" power state is selected when the monitors are in the dpms off state.
1. "high" forces the gpu to be in the "high" power state all the time. The "low" power state is selected when the monitors are in the dpms off state. The "profile" method is not as agressive as "dynpm," but is currently much more stable and flicker free and works with multiple heads active.

### The “dpm”  method : Dynamic power management

The "dpm" method uses hardware on the GPU to dynamically change the clocks and voltage based on GPU load. It also enables clock and power gating.
Power management is supported on all asics (r1xx-evergreen) that include the appropriate power state tables in the vbios; not all boards do (especially older desktop cards). "dpm" is only supported on R6xx and newer asics.

* Tip: DPM works on R6xx gpus, but is not enabled by default in the kernel (only R7xx and up). Cf model numbers in [2].

*  With the radeon driver, power saving is disabled by default and has to be enabled manually if desired.

* Unlike dynpm, the "dpm" method uses hardware on the GPU to dynamically change the clocks and voltage based on GPU load. It also enables clock and power gating.

There are 3 operation modes to choose from:
1. battery lowest power consumption
1. balanced sane default
1. performance highest performance

There are 3 performance modes : 
1. auto default; uses all levels in the power state
1. low enforces the lowest performance level
1. high enforces the highest performance level

# Steps to set different power management settings : 

The pm code supports three basic methods:

1. “dynpm” : is an old method.
1. “profile” : is rather static setting, not much dynamic change but may be the best to make sure laptop will keep at low gpu power/frequency.
1. “dpm” : latest dynamic power management method for the GPU AMD/ATI Radeon.

## Improved extracts from [2] + [5] : 

You can select the methods via sysfs [ie via modifying configuration files]. 

### For “dynpm” and “profile” methods : 

Make sure via “sudo gedit /etc/default/grub” that : 
* GRUB_CMDLINE_LINUX_DEFAULT="quiet splash" ie does not contain “radeon.dpm=1”.
* if modified --> “sudo update-grub”, then reboot.

`Echo "dynpm" or "profile" to /sys/class/drm/card0/device/power_method. `

However it will fail due to permission access rights.

[1] provides a solution for this : for those kind of “permission denied” issues, one of the solution is to do as below for instance : 

`echo "profile" | sudo tee /sys/class/drm/card0/device/device/power_method`

The other solution would be to be root/su users in order to be able to edit this kind of configuration file.

Then you can configure the “dynpm” or “profile” methods with the power_profile files to set the profiles corresponding to the methods you choose : 

For instance :
 
`echo "low" | sudo tee /sys/class/drm/card0/device/power_profile`

Please note that the 2 above files modifications are only valid during current session and will be overwritten at next laptop boot. You need to proceed to following steps to make those power method and profile choices permanent for future reboots : 
* Configure file /etc/rc.local
* This file for me was not even existing.
* I needed to log as “su” to create it following.
* Please refer to links [3] or [4] if file /etc/rc.local does not exist yet on your system.
* Add the configuration lines  before the last line of the file (exit 0), for instance : 

`(sleep 30 ; echo low > /sys/class/drm/card0/device/power_profile) &`

`(sleep 35 ; echo dynpm > /sys/class/drm/card0/device/power_method) &`

### For "dpm" method : 

It must be selected at boot (via radeon.dpm=1) and it is only supported on R6xx and newer asics. To know what are R6xx and newer asics, please see [2].

`“sudo gedit /etc/default/grub”`

Add this variable with radeon.dpm=1

`GRUB_CMDLINE_LINUX_DEFAULT="quiet splash radeon.dpm=1"`

if grub file changed, → “sudo update-grub” and reboot laptop.

For more configuration, 2 files are used. Note that those files are not available if computer is started in non dpm mode.

Those 2 files will be visible at the 1st reboot of the laptop with dpm mode activated or at following reboots.

`/sys/class/drm/card0/device/power_dpm_state`

can take values : battery, balanced, performance.

`/sys/class/drm/card0/device/power_dpm_force_performance_level`

can take values : auto, low, high.

To configure specific dpm state and performance to low, do the following : 

`echo battery | sudo tee /sys/class/drm/card0/device/power_dpm_state`

`echo low | sudo tee /sys/class/drm/card0/device/power_dpm_force_performance_level`

Commandline Tools : 
[radcard](https://github.com/superjamie/snippets/blob/master/radcard) - A script to get and set DPM power states and levels

For persitent configuration, follow same method as decribed above with /etc/rc.local file

Note that [5] gives another way to configure those GPU power settings permanently.

Graphical tools :
[Radeon-Tray](https://github.com/StuntsPT/Radeon-tray) — A small program to control the power profiles of your Radeon card via systray icon. It is written in PyQt4 and is suitable for non-Gnome users. 


# Sources : 
[1] : https://ubuntuforums.org/showthread.php?t=2149966 : 
* Forum discussion, source of most of my crucial findings.

[2] : http://www.x.org/wiki/RadeonFeature#...gement_Options
* 2nd source where I started to find about
 ◦ Type of AMD/ATI GPU / name / marketing name
 ◦ KMS Power Management options
     ▪ dpm
     ▪ profile
     ▪ dynpm 

[3] : https://forum.ubuntu-gr.org/viewtopic.php?p=247573
* Page in Russian but can be automatically translated if using Google Chrome and its translation options.
* Used to find out the /etc/rc.local file to permanently configure dpm/dynpm/profile options.

[4] : https://www.techfry.com/linux-tutorial/how-to-enable-etc-rc-local-for-running-commands-on-linux-boot
* Helping to create the /etc/rc.local init configuration file.

[5] : https://wiki.archlinux.org/index.php/ATI
* Very nice explanations as well about dpm/profile/dynpm methods, sometimes using same sources as [1].

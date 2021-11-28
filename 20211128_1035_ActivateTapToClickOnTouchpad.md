# Activate tap to click on touchpad

On Dell D430, using Ubuntu or Lubuntu or Debian, the tap on Touchpad does not work with basic Linux install.

I had to follow those steps to enable it, due to following information : " In recent systems (2017) as many distros are moving to Wayland, synaptics driver is no longer used. Instead, libinput is used."

To enable tap to click on touchpad using libinput create a file in Xorg config:

`$ touch /etc/X11/xorg.conf.d/99-synaptics-overrides.conf`

And add the following configuration:

```
Section  "InputClass"
    Identifier  "touchpad overrides"
    Driver "libinput"
    MatchIsTouchpad "on"
    Option "Tapping" "on"
    Option "TappingButtonMap" "lmr"
EndSection
```

source : https://unix.stackexchange.com/questions/337008/activate-tap-to-click-on-touchpad

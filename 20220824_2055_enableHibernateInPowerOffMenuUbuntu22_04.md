# Enable Hibernate In PowerOff Menu Ubuntu 22.04

Just after upgrading from Ubuntu 20.04 to Ubuntu 22.04, I had to re-enable `sudo hibernate` to work by adding again the following line into `/etc/sudoers` file:

```
# Add hibernate command to sudoers list /etc/sudoers.tmp
remi ALL=NOPASSWD:/usr/sbin/hibernate
```

Also, I succeeded to add Hibernate into poweroff menu by following a section from this page: https://github.com/arelange/gnome-shell-extension-hibernate-status

```
Hibernation button does not show up, but systemctl hibernate works
If you are running Ubuntu, try putting

[Enable hibernate in upower]
Identity=unix-user:*
Action=org.freedesktop.upower.hibernate
ResultActive=yes

[Enable hibernate in logind]
Identity=unix-user:*
Action=org.freedesktop.login1.hibernate;org.freedesktop.login1.handle-hibernate-key;org.freedesktop.login1;org.freedesktop.login1.hibernate-multiple-sessions;org.freedesktop.login1.hibernate-ignore-inhibit
ResultActive=yes
into /etc/polkit-1/localauthority/10-vendor.d/com.ubuntu.desktop.pkla
```

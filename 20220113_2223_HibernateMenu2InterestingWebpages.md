# Hibernate menu : 2 interesting webpages

- https://github.com/arelange/gnome-shell-extension-hibernate-status.

  - It shows how to enable the menus Hibernate, hybrid-sleep and sleep.
  - However both Hibernate and Sleep do not work, only hybrid-sleep works

Following the workaround from the FAQ.. copy paste the below content in the file /etc/polkit-1/localauthority/10-vendor.d/com.ubuntu.desktop.pkla

[Enable hibernate in upower]
Identity=unix-user:*
Action=org.freedesktop.upower.hibernate
ResultActive=yes

[Enable hibernate in logind]
Identity=unix-user:*
Action=org.freedesktop.login1.hibernate;org.freedesktop.login1.handle-hibernate-key;org.freedesktop.login1;org.freedesktop.login1.hibernate-multiple-sessions;org.freedesktop.login1.hibernate-ignore-inhibit
ResultActive=yes
Open the file with below command

 sudo -H gedit /etc/polkit-1/localauthority/10-vendor.d/com.ubuntu.desktop.pkla
Copy paste the above content, save the file and close..

Reboot & Test it..

- https://askubuntu.com/questions/1260527/hibernate-button-on-ubuntu-20-04.

  - It shows how to use extensions app to try to enable Hibernate buttons in the menus


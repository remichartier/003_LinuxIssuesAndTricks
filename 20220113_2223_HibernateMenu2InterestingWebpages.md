# Hibernate menu : 3 interesting webpages

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

- https://tipsonubuntu.com/2017/04/13/shutdown-hibernate-ubuntu-17-04-lid-closed/

gedit /etc/systemd/logind.conf

When the files opens, uncomment the line #HandleLidSwitch=suspend by removing # at its beginning, and change the value to:

HandleLidSwitch=poweroff, shutdown / power off Ubuntu when lid is closed.
HandleLidSwitch=hibernate, hibernate Ubuntu when lid is closed.
HandleLidSwitch=ignore, do nothing.
HandleLidSwitch=suspend, suspend laptop when lid is closed.

Save the file and finally restart the Systemd service to apply changes via command:

systemctl restart systemd-logind.service

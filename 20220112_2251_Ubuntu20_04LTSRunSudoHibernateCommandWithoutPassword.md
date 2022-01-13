# Ubuntu 20.04 LTS : Run Sudo Hibernate command without password

- Solution found in https://www.reddit.com/r/archlinux/comments/bkp591/systemctl_suspend_and_hibernate_with_no_root/ among other pages on similar topic.

```
which hibernate
/usr/sbin/hibernate

sudo visudo /etc/sudoers
```
- Add the following line : 
`<username> ALL= NOPASSWD: /usr/bin/hibernate`

```
CTRL + O for saving
CTRL + X for quitting
```
And then next time I do a `sudo hibernate`, system will start hibernation process without asking for a password.

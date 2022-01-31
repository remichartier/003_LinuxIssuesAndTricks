# Ubuntu 20.04 LTS : Run Sudo Hibernate command without password

## 1st solution but it did not work for me 
- Solution found in https://www.reddit.com/r/archlinux/comments/bkp591/systemctl_suspend_and_hibernate_with_no_root/ among other pages on similar topic.
  
```
which hibernate
/usr/sbin/hibernate

sudo visudo /etc/sudoers
```
- Add the following line : 
`<username> ALL= NOPASSWD: /usr/sbin/hibernate`
- Note, I wonder if we should remove the spaces ?
`<username> ALL=NOPASSWD:/usr/sbin/hibernate`


```
CTRL + O for saving
CTRL + X for quitting
```
And then next time I do a `sudo hibernate` (or `hibernate`, system will start hibernation process without asking for a password.

## 2nd solution but not sure it worked for me
- Solution found in : https://giuseppe998e.medium.com/how-to-directly-reboot-from-linux-to-windows-e6f7d7c1a3fe

Replacing *USER* with your username and *PATH* with the path getted using `which hibernate`
```
which hibernate
/usr/sbin/hibernate

sudoedit /etc/sudoers/*USER*  -> it does not have this file ...
```
- Add 
```
*USER* ALL=(ALL) ALL
*USER* ALL=(root) NOPASSWD:*PATH*
```
- Save file (CTRL + O and CTRL + X)

# Linux / Windows 10 Dual Boot : How to directly reboot from Linux to Windows independently of the primary boot OS

Source : https://giuseppe998e.medium.com/how-to-directly-reboot-from-linux-to-windows-e6f7d7c1a3fe

1 — The new ALIAS
- Open ~/.bashrc or ~/.zshrc
- Add alias wreboot="sudo grub-reboot X && reboot" replacing the X with the position of the Windows entry in the GRUB list (starting from zero)
- Save file

2 — Update the GRUB
- Open /etc/default/grub
- Set the variable GRUB_DEFAULT as saved .
- Save file
- Execute sudo update-grub (on Ubuntu)
- Or sudo grub-mkconfig -o /boot/grub/grub.cfg (on ArchLinux)

3 — Get rid of SUDO password
- Replacing *USER* with your username and *PATH* with the path getted using which grub-reboot(ex: /usr/bin/grub-reboot):
- Open /etc/sudoers.d/*USER* with sudoedit
- Add *USER* ALL=(ALL) ALL
- And *USER* ALL=(root) NOPASSWD:*PATH*
- Save file

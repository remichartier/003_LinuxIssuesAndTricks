# Linux Erase Hard drives

- unmount the drive first

- Ex : `sudo umount /dev/sdb1 -l`

- Then either use `shred` or `dd` :
  - `sudo shred -vfz /dev/sdb` 
  - or
  - `sudo dd if=/dev/urandom of=/dev/sdb bs=10M`  

Note : make sure not to erase the wrong drive / the main hard drive !

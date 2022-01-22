# Ubuntu 20.04 : Full copy of one bootable SSD disk to another

- Source : https://www.howtogeek.com/howto/19141/clone-a-hard-drive-using-an-ubuntu-live-cd/

>>- Cloning hard drives is a common maintenance task.

>>- **dd** is a utility used to do low-level copying – rather than working with files, it works directly on the raw data on a storage device.

>>- List the disks recognized by the system : `sudo fdisk –l`

>>- We want to copy the data from /dev/sda to /dev/sdc.

>>  - Note: while you can copy a smaller drive to a larger one, you can’t copy a larger drive to a smaller one with the method described below.

>>- Use `dd` to make a raw copy of one disk into another. Example : `sudo dd if=/dev/sda of=/dev/sdc`. 

>>- In this case, we’re telling dd that the input file (“if”) is /dev/sda, and the output file (“of”) is /dev/sdc. If your drives are quite large, this can take some time.

>>- If we do `sudo fdisk –l` again, we can see that, despite not formatting /dev/sdc at all, it now has the same partitions as /dev/sda.

>>- Additionally, if we mount all of the partitions, we can see that all of the data on /dev/sdc is now the same as on /dev/sda.
>>  - Example : 
>>    - `sudo diff -rq /dev/sda1 /dev/sdc1`
>>    - `sudo diff -rq /dev/sda2 /dev/sdc2`

>>- Note: you may have to restart your computer to be able to mount the newly cloned drive.

>>- Unlike other utilities, dd copies absolutely everything from one drive to another – that means that you can even recover files deleted from the original drive in the clone!

I did this procedure. I was able to physically copy one bootable SSD to another, and boot on the copied SSD (Linux Ubuntu).



# Ubuntu 20.04 : Enable Hibernate on Lenove Ideapad 3i Gaming laptop

## Configure properly swapfile size

According to [1] : 
```
Hibernate saves all of your RAM data on the hard disk and restores back into RAM after you turn on the computer.
.....
That’s why the swap partition must be more than or equal to RAM. To check your swap partition open ‘System Monitor’.

In the Resources Tab check your RAM and Swap. If swap is more than RAM, you’re good to go
```

According to [2] : 

In order to do so, you must first disable the current swap space.

This action may take a minute or so to execute, so don’t panic!

`sudo swapoff -a`

You can now resize the swap space with fallocate. In this example, I am increasing it to 2GB. (But on my on laptop, needed to increase to 8G, equivalent to RAM size)

`sudo fallocate -l 2G /swapfile`

Now check how much swap space is configured with:

`ls -lh /swapfile`

Output:

`-rw------- 1 root root 2.0G Feb 13 03:12 /swapfile`

Above we can see there is now 2GB of swap space configured.

Make the swap file only accessible to root.

`sudo chmod 600 /swapfile`

Mark the file as a swap file.

`sudo mkswap /swapfile`

You may see a warning when resizing a previous swap file.
```
mkswap: /swapfile: warning: wiping old swap signature.
Setting up swapspace version 1, size = 2 GiB (2147479552 bytes)
no label, UUID=db0ee16f-a97f-4df0-a83e-713cd874a3fe
```
Finally we will tell the system to start using our new swap file.

`sudo swapon /swapfile`

To verify that the swap is now available, type:

`sudo swapon --show`


Output:
```
NAME      TYPE SIZE  USED PRIO
/swapfile file   2G 35.3M   -2
```
Above we can see a 2GB swap file available.

We can also run the following command to see our new swap file alongside physical memory.

`free -h`
```
              total        used        free      shared  buff/cache   available
Mem:           985M        674M         66M         61M        244M        110M
Swap:          2.0G         77M        1.9G
```
Your resized swap is ready to go!

If you can, reboot the server with sudo reboot and run sudo swapon --show again just to make sure the swap space was created automatically on startup.



## Sources : 
[1] : [How to Enable Hibernate in Ubuntu Linux](https://www.linuxandubuntu.com/home/how-to-enable-hibernate-in-ubuntu-linux)
  - Explain need for swap file or swap partition to be properly sized.

[2] : [How To Create or Resize Swap Space on Ubuntu 20.04 – 20.10 & 18.04 – 19.10](https://devanswers.co/creating-swap-space-ubuntu-18-04/)
  - Paragraph `Increase or Resize Swap Space`
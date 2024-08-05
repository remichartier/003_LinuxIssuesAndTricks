# Linux / Ubuntu : Automount 2nd hard drive with only specific user permissins instead of root owner giving permissions to all users

Sources:
- https://help.ubuntu.com/community/AutomaticallyMountPartitions#Per-User_Mounts

- Start Disks app
- Select the 2nd drive, and the partition mounted, or to be mounted.
- If mounted already, in my case, it is mounted in `/media/<user_id>/Data
- click on the Settings icon for this partition.
- Configure the following:
  -  User Session Default --> Off.
  -  Show in user interface --> On.
  -  Require additional authorization to mount --> On. (This helps mounting as "user_id" instead of "root" I think.
  -  Keep empty the fields "Display Name", "Icon Name", "Symbolic Icon Name"
-  Options: `nosuid,nodev,nofail,x-gvfs-show,uid=1000,x-udisks-auth,umask=077`
  - Explanations
    - Usually, default options are `nosuid,nodev,nofail,x-gvfs-show`
    - I added `uid=1000` to mount the disk as the 1st user id created when installing Ubuntu, instead of the "root" user.
    - The `x-udisks-auth` was added when checking the "Require additional authorization to mount"
    - I added `umask=077` to only allow <user_id> permissions, and remove permissions for Others an Group users.
- Mount point set to `/media/<user_id>/Data`, provided that the folders `/media/<user_id>/Data` already exist, it will mount the disk on the `Data` folder.

All those tricks allowed me to auto-mount the 2nd hard drive at every system startup, not as root with permissions to everyone, but instead as <user_id> with permissions to no one else, which is more secure in terms of blocking access to any unwanted users.

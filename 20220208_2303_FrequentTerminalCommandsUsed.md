# Frequent Terminal Commands Used

## Quick Find Terminal command :

`find . -type f -iname 201910*google*.pdf`

## Rename files :

```
rename 's/\-/\_/' *.jpg

sudo rename 's/IMG\-//' *.jpg

sudo rename 's/IMG\_//' *.jpg

sudo rename 's/VID\_//' *.mp4

sudo rename 's/2014/2015/' *.jpg
```

## Install .deb files

`sudo apt install -f`

## Grep options
```
-R or -r --> recursive
-i --> ignore case
-e --> use regex patterns for search
```

## tee

For redirecting in parallel stdout to a file
`<cmd> | tee log.txt`

## List of folder sizes

Source: https://superuser.com/questions/869969/is-there-a-terminal-command-to-list-folder-size-and-corresponding-file-sizes-wit

'''du -chd 1 | sort -h'''

It outputs the total size of each sub-directory from the current directory location (the "1" above), as well as a total of all sub-directories, and sorts it by human-readable sizes

'''du -m | sort -nr | head -10'''

It lists all folders (including repetitive sub-folders) with most disk space usage sorted.

here is the tree command. Install it via sudo apt-get install tree, and type the following:

'''tree -h'''

## Get list of packages installed on Ubuntu

Source: https://www.cyberciti.biz/faq/apt-get-list-packages-are-installed-on-ubuntu-linux/

```apt list --installed```

Get if a specific package is installed:

```apt list apache2```

## Check available ports on Ubuntu

Source: https://learnubuntu.com/check-open-ports/#:~:text=How%20to%20Check%20Open%20Ports%20in%20Ubuntu%201,open%20files.%20...%203%203.%20Using%20ss%20Command

```
sudo ss -ltunp |grep 8080

sudo ss -ltunp

ss -ltunp

```


## Docker commands

### Checking Docker disk space usage [The Docker Way]

Source https://linuxhandbook.com/docker-disk-space-usage/

```docker system df```

More details:
```docker system df -v```

### Checking docker image sizes
```docker image ls```

Source https://stackoverflow.com/questions/18497688/run-a-docker-image-as-a-container#:~:text=Do%20the%20following%20steps%3A%201%20%24%20docker%20images,can%20also%20specify%20an%20image%20ID%20%28no%20tag_name%29.

```docker images```

You will get a list of all local Docker images with the tags specified.

```docker run image_name:tag_name```

If you didn't specify tag_name it will automatically run an image with the 'latest' tag.

Instead of image_name, you can also specify an image ID (no tag_name).

### Stop, start, and name containers

Source https://docs.docker.com/language/nodejs/run-containers/

Docker containers can be started, stopped and restarted. When we stop a container, it is not removed but the status is changed to stopped and the process inside of the container is stopped. When we ran the docker ps command, the default output is to only show running containers. If we pass the `--all` or `-a` for short, we will see all containers on our system whether they are stopped or started.

```docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                      PORTS               NAMES
ce02b3179f0f        node-docker         "docker-entrypoint.s…"   16 minutes ago      Exited (0) 5 minutes ago                        wonderful_kalam
ec45285c456d        node-docker         "docker-entrypoint.s…"   28 minutes ago      Exited (0) 20 minutes ago                       agitated_moser
fb7a41809e5d        node-docker         "docker-entrypoint.s…"   37 minutes ago      Exited (0) 36 minutes ago                       goofy_khayyam
```

Now, list all the containers again using the ps command.

```docker ps --all```

```docker stop wonderful_kalam```

Now that all of our containers are stopped, let’s remove them. When a container is removed, it is no longer running nor is it in the stopped status. However, the process inside the container has been stopped and the metadata for the container has been removed.

To remove a container, simply run the docker rm command passing the container name. You can pass multiple container names to the command in one command.

Again, make sure you replace the containers names in the below command with the container names from your system.

```docker rm wonderful_kalam```

Run the docker ```ps --all``` command again to see that all containers are gone.

### Run GUI applications from Docker

Source: https://www.geeksforgeeks.org/how-to-run-gui-based-applications-inside-docker/#:~:text=How%20to%20Run%20GUI%20Based%20Applications%20inside%20Docker%3F,install%20firefox%2C%20jupyter%20%26%20gedit.%20...%20More%20items

### Accessing volume folder eventhrough no access rights to /var/lib/docker folder on Ubuntu

Idea is to use another container with /bin/bash access, mount it on the volume, and access to this volume via this container. Example:
`docker run -it -v floating-server-volume:/mnt ubuntu /bin/bash`



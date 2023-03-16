# Frequent Linux/Ubuntu Terminal Commands Used

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

`sudo apt install -f package_file.deb`

Sometimes, I found this above command not working, so I used this one instead:
`sudo dpkg -i package_file.deb`

## Grep options
```
-R or -r --> recursive
-i --> ignore case
-e --> use regex patterns for search
-v --> exclude pattern
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
## Get computer IP address or DNS name
```
hostname

hostname -I

ip addr

ifconfig
```

## Unzip a 7z file (7zip)

Source: https://askubuntu.com/questions/219392/how-can-i-uncompress-a-7z-file

First install the according package sudo apt install p7zip-full

use x flag to extract files with full path
use -o flag to set output directory
7z x <archive_name> -o{Directory}

for example

7z x file.7z -o/home/michael/Documents/NewFolder

Notice that there is no space between -o and the output directory. If the file was encrypted, it will automatically ask for the password.


## Docker commands

### What is docker?

Source: https://www.simplilearn.com/tutorials/docker-tutorial/how-to-install-docker-on-ubuntu

* A tool that is used to automate the deployment of applications in lightweight containers so that applications can work efficiently in different environments. 
* Multiple containers run on the same hardware
* Maintains isolated applications

### Interesting Docker information sources / links

* https://www.digitalocean.com/community/tutorials/how-to-remove-docker-images-containers-and-volumes
* https://docs.docker.com/language/nodejs/run-containers/
* https://www.geeksforgeeks.org/how-to-run-gui-based-applications-inside-docker/
* https://www.kosli.com/blog/docker-commit-explained-a-guide-with-examples/
* https://stackoverflow.com/questions/52980617/how-to-re-enter-to-docker-containter-prompt-after-exiting
* https://vsupalov.com/6-docker-basics/ --> Docker images, containers, volumes, dockerfiles

### Difference images/containers, build images, run containers, run in detached mode, 

Source: https://docs.docker.com/language/nodejs/run-containers/

We created our image using the command docker build. Now that we have an image, we can run that image and see if our application is running correctly.

A container is a normal operating system process except that this process is isolated and has its own file system, its own networking, and its own isolated process tree separate from the host.

To run an image inside of a container, we use the docker run command. The docker run command requires one parameter and that is the image name.

Source: https://www.kosli.com/blog/docker-commit-explained-a-guide-with-examples/

An Overview of Basic Terms

* Image: An image is a set of files, including the source/binaries and configuration needed for the application to run. An image is read only. We can create one by providing a Dockerfile to the docker build command. We can also create an image with the commit command from a container.

* Container: A container is a version of the image, ready to run as an application. It contains the environment for the application to run (e.g., file systems, environment variables, port mappings, etc.). We can use either the create or run commands to create a container from an image. Create will only create the container, whereas run will also start it. A container need not be running once created; it can also be in the stopped state. The docker ps command lists the created containers.

Source: https://stackoverflow.com/questions/52980617/how-to-re-enter-to-docker-containter-prompt-after-exiting

When you run following command it performs 2 operations.

$ docker run -p 8081:80 --name eg -it epgg/eg bash
It creates a container named eg
It has only one purpose/process bash that you have overridden using cmd parameter.
That means when bash shell is over/complete/exit container has no objective to run & hence your docker container will also entered into stopped stage.
Ideally you should create a container to run apache-server as the main process (either by default entry-point or cmd).

$ docker run -p 8081:80 --name eg -d epgg/eg
And then using following command you can enter inside the running container.

$ docker exec -it eg bash
here name of your container is eg (Note since you already have a container named "eg" you may want to remove it first)

### Docker run -it -d, docker exec, /bin/bash, -v for volumes

Source: https://stackoverflow.com/questions/18497688/run-a-docker-image-as-a-container#:~:text=Do%20the%20following%20steps%3A%201%20%24%20docker%20images,can%20also%20specify%20an%20image%20ID%20%28no%20tag_name%29.

Examples:
```
 docker run -i -t ubuntu:12.04 /bin/bash
 
 docker run image_name:tag_name
 
 docker run -d --restart=always -p 8080:80 image_name:version

docker exec -it container_id /bin/bash

docker run -d --name  container-name -p localhost:80:80 -v $HOME/myContainer/configDir:/myImage/configDir --restart=always image-name
Where:

--detach , -d        Run container in background and print container ID
--name                Assign a name to the container
--publish , -p        Publish a container’s port(s) to the host
--volume , -v        Bind mount a volume
--restart            Restart policy to apply when a container exits
```

There are two ways to run the image in the container:

$ docker run [OPTIONS] IMAGE[:TAG|@DIGEST] [COMMAND] [ARG...]
In detached mode:

-d=false: Detached mode: Run container in the background, print new container id
In interactive mode:

-i :Keep STDIN open even if not attached

### Exiting a container

Soources: 
* https://vsupalov.com/exit-docker-container/#:~:text=Exiting%20a%20Docker%20Container%201%20Just%20Stopping%20the,Alternative%20Workflow%20...%204%20Your%20Road%20Ahead%20
* https://phoenixnap.com/kb/exit-docker-container#:~:text=Method%201%3A%20Exit%20and%20Stop%20Docker%20Container,-Perform%20the%20following&text=If%20a%20process%20is%20running,exit%20and%20stop%20the%20container.

* If there’s a non-shell process running --> CTRL + C to interrupt it. Then CTRL + D
* Otherwise, "exit" or CTRL + D to exit stop and exit a container.

* If wanting to keep the container running in the background:
  * Start the container with -d flag (to be able to "daemonize" the container)
  * Then CTRL + P and CTRL + Q (turns interactive mode to daemon mode, which keeps the container running but frees up the terminal)
  * You can attach to it later using docker attach, if you need to interact with the container more `docker attach [container-name-or-id]`

### Launch several sessions connected to the same container

Source: https://stackoverflow.com/questions/39794509/how-to-open-multiple-terminals-in-docker#:~:text=You%20can%20run%20docker%20exec,connected%20to%20the%20same%20container.

You can run `docker exec -it <container> bash` from multiple terminals to launch several sessions connected to the same container.
 
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

Remove image by Image ID:
```docker rmi [imageID]```

Run the docker ```ps --all``` command again to see that all containers are gone.

### List specific docker container status

```docker ps --filter name="name of the container"```

### Run GUI applications from Docker

Source: https://www.geeksforgeeks.org/how-to-run-gui-based-applications-inside-docker/#:~:text=How%20to%20Run%20GUI%20Based%20Applications%20inside%20Docker%3F,install%20firefox%2C%20jupyter%20%26%20gedit.%20...%20More%20items

### Accessing volume folder eventhrough no access rights to /var/lib/docker folder on Ubuntu

Idea is to use another container with /bin/bash access, mount it on the volume, and access to this volume via this container. Example:
`docker run -it -v floating-server-volume:/mnt ubuntu /bin/bash`

### Run docker container in background and access it later
Example:
```
docker run -d --name <container_name> -v <volume_name>:/data <docker_image_name>

docker exec -it  <container_name_or_ID> /bin/bash
```
When exiting docker, container will continue to keep active and will not exit

### Docker stop/restart/rm container
First get the list of containers, with their names and IDs, then use docker commands to stop/start/restart/rm them
```
docker ps -a

docker (start/stop/rm) <container_name_or_id>
```
Source: https://stackoverflow.com/questions/21928691/how-to-continue-a-docker-container-which-has-exited
```
docker start -a -i `docker ps -q -l`
Explanation:

docker start start a container (requires name or ID)
-a attach to container
-i interactive mode
docker ps List containers
-q list only container IDs
-l list only last created container
```
I used:
`docker (start/stop/rm) -a -i <container_name_or_id>` to start again an exited /bin/bash container

### Ubuntu: where docker files are created?

Generally, /var/lib/docker

### Upload file to a docker container

Source: https://wangler.io/upload-a-file-to-a-docker-container/

```
docker cp missing_data.sql <container-id>:/missing_data.sql

```
### Docker: how to check that the NVIDIA Container Toolkit is installed

Source: https://github.com/moby/moby/issues/40903
```
which nvidia-container-toolkit
```
### Docker: disk out of space
Use:
```docker system prune```
* it removes unused data, clears unused images, containers.
```
docker system prune
WARNING! This will remove:
  - all stopped containers
  - all networks not used by at least one container
  - all dangling images
  - all dangling build cache

Are you sure you want to continue? [y/N] 
```

## Get Nvidia GPU infos

On Linux: `nvidia-smi`

## Measure time duration of a command

`time command`

Result example:
```
real	2m6.356s
user	1m5.299s
sys	0m13.693s
```






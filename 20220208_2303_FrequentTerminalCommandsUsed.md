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
## Remove files recursively without deleting folders
Source: https://unix.stackexchange.com/questions/182033/remove-all-files-recursively-without-deleting-directories
```
find . ! -name '.*' ! -type d -exec rm -- {} +
```

## Install .deb files

`sudo apt install -f package_file.deb`

Sometimes, I found this above command not working, so I used this one instead:
`sudo dpkg -i package_file.deb`

## Uninstall packages installed with dpkg -i
Source: https://unix.stackexchange.com/questions/195794/how-to-uninstall-a-deb-installed-with-dpkg
```
dpkg -l package_name    (check if this package is correctly installed in your system and being listed by dpkg tool)
dpkg -r package_name    (remove the package itself (without the configuration files))
dpkg -P package_name    (delete (purge) the package completely (with configuration files))
dpkg -l                 (check if the package has been removed successfully)
```

## See what "apt" would install without actually doing it
Source: https://makandracards.com/makandra/1142-debian-ubuntu-see-what-apt-would-install-without-actually-doing-it

`sudo apt-get install --dry-run something`

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

## Terminal output redirection
Source: https://askubuntu.com/questions/420981/how-do-i-save-terminal-output-to-a-file

if you want to have both stderr and output displayed on the console and in a file use this:

`SomeCommand 2>&1 | tee SomeFile.txt`

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
- Get both dns name and IP address or a computer DNS name: `getent hosts xxx.xxx.xxx.com`

## Unzip a 7z file (7zip)

Source: https://askubuntu.com/questions/219392/how-can-i-uncompress-a-7z-file

First install the according package sudo apt install p7zip-full

use x flag to extract files with full path
use -o flag to set output directory
7z x <archive_name> -o{Directory}

for example

7z x file.7z -o/home/michael/Documents/NewFolder

Notice that there is no space between -o and the output directory. If the file was encrypted, it will automatically ask for the password.

## Get Nvidia GPU infos, check GPU/Vulkan info via command line (both Ubuntu and Windows10)

On Linux: `nvidia-smi`

To get GPUs: `nvidia-smi -L`

`vulkaninfo`

## Measure time duration of a command

`time command`

Result example:
```
real	2m6.356s
user	1m5.299s
sys	0m13.693s
```
## Alternative to 'ps - aef'
`pgrep simu -l`: it will return any process name containing "simu", with its process ID. If needing to stop it, we can then use the process ID to kill it.

## Format a json file
Source: https://stackoverflow.com/questions/5243885/json-command-line-formatter-tool-for-linux#:~:text=On%20Ubuntu%20jsonlint%20is%20provided%20by%20apt%3Apython3-demjson%20Usage%3A,-y%20python3-demjson%20%24%20jsonlint%20-f%20input.json%20%3E%20output.json

On Ubuntu jsonlint is provided by apt:python3-demjson.
Usage:
```
$ sudo apt install -y python3-demjson
$ jsonlint -f input.json > output.json
```
## sed Stream string Editor

Good source: https://www.howtogeek.com/666395/how-to-use-the-sed-command-on-linux/

## Fixing an incompatible nvidia-driver package insall
Context: on Ubuntu 20.04, via the Software Installer, I tried to install the latest Nvidia driver 535. Unfortunately, dependency issues makes it not compatible with Ubuntu 20.04, with some Nvidia kernal dependencies.
- `nvidia-smi` command was telling the nvidia-driver-535 was not compatible with the Nvidia NVLM library installed: `Failed to initialize NVML: Driver/library version mismatch`
- Display resolution was stuck at 800x600.
- `sudo apt remove nvidia-driver-535` was reporting some dependency issues with other packages.

Resolution: 
- Remove all the Nvidia installed packages: `sudo apt-get --purge remove "*nvidia*"`, however, this command fails due to dependencies on other packages.
- `sudo nvidia-uninstall` to uninstall manually installed drivers.
- If blocked by dependencies, use `sudo gedit /var/lib/dpkg/status`, need to manually edit the dpkg status file, and look for the problematic package name. Remove those packages and save the file (Source: https://askubuntu.com/questions/1279472/i-cant-remove-packages-that-have-unmet-dependencies). Until the command `sudo apt-get --purge remove "*nvidia*"` completes successfully.
- If some dependency packages are holding the removal, we can remove the holds: `sudo apt-mark unhold package_name` (source https://askubuntu.com/questions/164587/how-can-you-unhold-remove-a-hold-on-a-package#:~:text=You%20can%20use%20sudo%20apt-mark%20unhold%20package_name.%20The,you%20can%20use%20sudo%20apt-mark%20unhold%20%24%28apt-mark%20showhold%29.)
- Check that all has been removed with `dpkg -l |  grep -i nvidia`,  if anything still has `ii` in the leftmost column, then purge it too. (source https://askubuntu.com/questions/1482917/ubuntu-20-04-doesnt-load-after-installing-nvidia-535-driver-and-stuck-at-black)
- Re-install the original nvidia-driver compatible with Ubuntu 20.04: `sudo apt install nvidia-driver-525`.
- If successfull, reboot. The machine should reboot with a normal resolution, and `nvidia-smi` should not return and warning/error message any more.
- Clean the installed/unused packages:
  - `sudo apt --fix-broken install` or `sudo apt-get install -f` or `sudo dpkg --configure -a` (repair commands)
  - `sudo apt autoremove`
  - `sudo apt autoclean` 

## Ubuntu clean apt installed / unused packages
- `sudo apt autoremove`
- `sudo apt autoclean` 

## Install Ubuntu drivers

Rely on automatic detection, which will install the driver that is considered the best match for your hardware: `sudo ubuntu-drivers install` (source https://ubuntu.com/server/docs/nvidia-drivers-installation)

## CMAKE generated dynamic libraries and executable in bin/debug instead of bin folder
Sources: 
- https://stackoverflow.com/questions/19024259/how-to-change-the-build-type-to-release-mode-in-cmake
- https://iamsorush.com/posts/cpp-cmake-build/

CMAKE on Windows with generate in debug mode in /bin/debug folder.
On Windows, if switching to release mode via command `cmake --build {DIR} --config Release`, it will generate executables/libraries to bin/Release folder

## Shell script 'pushd/popd' quiet mode
`pushd <folder> > /dev/null`

`popd > /dev/null`

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

Source: https://medium.com/codex/running-gui-applications-in-docker-firefox-nautilus-file-manager-5424694104ec
Example to run Nautilus on a Docker container.
Run the docker container with options: `-e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix`
Example of Firefox: Add `--net=host`

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
When docker container is "exited", we can restart the container with:
`docker restart <container_id>`
Then enter the docker container with:
`docker exec -it  <container_name> /bin/bash`

### Ubuntu: where docker files are created?

Generally, /var/lib/docker

### Upload/Download files or folders To/From a docker container

Source: https://wangler.io/upload-a-file-to-a-docker-container/

```
docker cp missing_data.sql <container-id>:/missing_data.sql

docker cp <container-id>:/missing_data.sql missing_data.sql

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
### Docker: Run executable from host within docker container
Source: https://stackoverflow.com/questions/30362373/run-executable-from-host-within-docker-container

Mount the executable into the container with a volume like this:

`$ docker run -v /path/to/executable:/my_exe debian /my_exe`

The only problem is you will also need to take care of making sure any required libraries are also available in the container.

### Docker: Adapting TZ variable to US PST time
Context: In docker file:
```
ENV TZ="Europe/Budapest"
```
To adapt to local computer, check its timezone via `cat /etc/timezone`
Replace its result in the TZ variable:
```
ENV TZ="America/Los_Angeles"
```

### Dockerfile command to update Cmake to latest version

```
RUN apt-get update && apt-get install -y python3-pip && \
	 pip install cmake --upgrade
```

### Dockerfile: install gedit and nautilus

```
RUN apt-get install -y nautilus
RUN apt install -y gedit
```

### Dockerfile: install a .def file into docker image

```
ENV FILE=filename.deb
COPY $FILE /tmp
RUN dpkg -i /tmp/$FILE && \
    rm -rf /tmp/$FILE
```

### Dockerfile: copy a .zip file to a Docker image and unzip it

```
ENV FILE=file.zip
COPY $FILE /root
RUN unzip /root/$FILE -d /root/ros
```

### see docker build logs

C.f. tricks here: https://forums.docker.com/t/capture-ouput-of-docker-build-into-a-log-file/123178
















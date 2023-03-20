## Installation of software

<pre font-family="Cascadia Code">
      +-----------------------------------+
    | |     Download the installer        |
    | |-----------------------------------|
    | |        Run the installer          |
    | |-----------------------------------|
    | | Error Message during installation |<--+
    | |-----------------------------------|   |
    | |   Troubleshooting the issue       |   |
    | |-----------------------------------|   |
    | |     Re-Run the installer          |   |
    | |-----------------------------------|   |
    V |       Get another error           |---+
      +-----------------------------------+ </pre>

## Images and Containers

- **Docker Image** is a file which contains all the necessary dependency and configurations which are required to run an applicaion.
- **Docker Containers** is basically a running instance of an image

- <pre font-family="Cascadia Code">
                             +------------+
                    ,--------| Container  |
  +-----------+    /         +------------+
  |   Image   |---<          +------------+
  +-----------+    `---------| Container  |
                             +------------+</pre>

## Port binding

- By default Docker container can make connections to the outside world, but the outside world cannot connect to containers.
- If we want containers to accept incoming connection from the world, you will have to bind it to a host port.
- <pre font-family="Cascadia Code">
        _______________________________
      [ ]           ._______.         |
      [ ]---------->| nginx | Port 80 |
      [ ] Post 8080 '-------'         |
        |_____________________________|
            Docker Host</pre>

## Overview of docker container exec

- The docker container exec command runs a new command is a running container.
- The command started using docker exec only while the container's primary process (PID 1) is running, and it is not restarted if the container is restarted.
- <pre font-family="Cascadia Code">
        .------------------------------.
       [ ]     ._______.     bash      |
  -----[-]---->| nginx |               |
  Pid 1[ ]     '-------'     ping      |
        '------------------------------'
          Nginx  Docker Container </pre>

## Docker commands

- Whenever we run a continer, a default command executes which typically runs as PID 1 .This command is present in the docker file. This command can be defined while we are defining the container image.

### Some commands

- docker pull nginx
- docker run --name myname -p 8080:80 -dt nginx
- docker ps -a
- docker start myname {name}
- docker start 84a983b9b463f9a83114d4ff454fc4f10aca9f5794e5d713f49490736155206a {uuid}
- docker stop myname {name}/{uuid}
- docker images
- docker inspect myname
- docker container stop myname
- docker container ls -aq
- docker container stop $(docker container ls -aq)
- docker container rm myname {name}/{uuid}
- docker container exec -it myname bash
- docker container exec -it myname netstat -ntlp
- docker container create busybox
  **create** command creates a fresh new container from a docker image. However, it doesn’t run it immediately.
- docker container start myname
  **start** command will start any stopped container. If you used docker create command to create a container, you can start it with this command.
- docker container run -dt busybox
  **run** command is a combination of create and start as it creates a new container and starts it immediately. In fact, the docker run command can even pull an image from Docker Hub if it doesn’t find the mentioned image on your system.
- docker container run -d nginx sleep 20
  **Overriding default** container command but show's original on (docker ps)
- docker rm myname
  Remove the container from disk
- docker system df
  Gives space of each images, containers, local volume & cache
- docker system df -v
  Gives per component level size
- docker container run -dt --name testcontainer busybox ping -c10 google.com
- docker container run -dt -rm --name testcontainer busybox ping -c10 google.com
  Adding **rm** option on starting to remove the container on being executed
- docker build -t name. {specify the directory}
  The image created will be stored in docker
- 
 
## Docker restart policies

- By default, Docker container will not start when they exit or when docker daemon is restarted. Docker provides restart policies whether your container start automatically when they exit, or when Docker reastarts.
- We can specify the restart policy by using the --restart flag with docker run command.

Flag          |     Desciption        |
--------------|-----------------------|
no            |Do not automatically restart the container (the defalut) |
on-failure    |Restart the container if it exits due to an error, which manifests as a non-zero exit code |
unless-stopped|Restart the container unless explicitly stopped or Docker itslef is stopped or restarted |
always        | Always restart the container if it stops

### Command strings

Abbreviation | Complete string |
-------------|-----------------|
 -a  | --all
 -p  | --port
 -d  | --detached
 -a  | --attached
 -i  | --interactive
 -t  | --tty

## Docker Images

- A **Dockerfile** is a text document that contain all the commands a user could call on the command line to assemble an image.
- Sample content of docker file
  <pre font-family="Cascadia Code">
  FROM ubuntu
  RUN apt-get update
  RUN apt-get install nginx -y
  CMD ["nginx", "-g", "daemon off"]</pre>

- Commands
  - FROM : Build the docker image with specific command
  - RUN : run the specific instruction
  - CMD : start the container with specified command.
  - Copy and Add are both dockerfile instruction that serve similar purposes of copying files from a specific location into a Docker image
  - COPY : takes in a src and destination.  It only copy in a local file or directory from your host.
  - ADD : lets you do two additional operations
    - use a URL instead of a local file / directory.
    - extract a tar file from the source directory into the destination.
  - Using ADD to fetch package from remote URLs is strongly discouraged, instead use **curl** or **wget**.
  - EXPOSE : informs Docker that the container listens on the specified network ports at runtime without actually publishing the port.
  - It *functions as a type of documentation* between the person who build the image and
  the person who runs the continer, about which ports are intended to be published.

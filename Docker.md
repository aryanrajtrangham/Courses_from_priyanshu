# Docker

## Installation of software

```[]
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
      +-----------------------------------+ 
```

## Images and Containers

- **Docker Image** is a file which contains all the necessary dependency and configurations which are required to run an applicaion.

- **Docker Containers** is basically a running instance of an image

- ```[]
                             +------------+
                    ,--------| Container  |
  +-----------+    /         +------------+
  |   Image   |---<          +------------+
  +-----------+    `---------| Container  |
                             +------------+
  ```

## Port binding

- By default Docker container can make connections to the outside world, but the outside world cannot connect to containers.

- If we want containers to accept incoming connection from the world, you will have to bind it to a host port.

- ```[]
        _______________________________
      [ ]           ._______.         |
      [ ]---------->| nginx | Port 80 |
      [ ] Post 8080 '-------'         |
        |_____________________________|
            Docker Host
  ```

## Overview of docker container exec

- The docker container exec command runs a new command is a running container.

- The command started using docker exec only while the container's primary process (PID 1) is running, and it is not restarted if the container is restarted.

- ```[]
        .------------------------------.
       [ ]     ._______.     bash      |
  -----[-]---->| nginx |               |
  Pid 1[ ]     '-------'     ping      |
        '------------------------------'
          Nginx  Docker Container
  ```

## Docker commands

- Whenever we run a continer, a default command executes which typically runs as PID 1 .This command is present in the docker file. This command can be defined while we are defining the container image.

### Some commands

- docker pull nginx
  </br>Pull an image from docker seerver

- docker run --name {name} -p 8080:80 -dt {base-image}
  </br>Running an image by the name myname on port 80 of container diverted to 8080 of running machine (computer/server).

- docker container ps -a
  </br>docker ps -a
  </br>Displays all the container that are run

- docker image ls
  </br>docker images
  </br>To display all images (of container) present.

- docker image inspect {name}
  </br>To inspect an image, the returned json object contain lots of information regarding the image with given name or id

- docker start {name}/{id}
  </br>To start a container with given name or id

- docker container start {name}/{id}
  </br>To start a container in stop state present in the containers with given name or id

- docker stop {name}/{id}
  </br>docker container stop {name}/{id}
  </br>To stop a container with given name or id

- docker container ls -aq
  </br>List all the images present in the containers

- docker container stop $(docker container ls -aq)
  </br>To stop all the images present in the containers

- docker container rm {name}/{id}
  </br>docker rm {name}/{id}
  </br>To remove containers with given name name or id

- docker container exec -it {name} {command}
  </br>To execute a command on the image running container.
  </br>Example: docker container exec -it myname netstat -ntlp

- docker container run -d --restart unless-stopped nginx
 </br>The docker runs and restarts unless stopped

- docker container create {name}
  </br>Create command creates a fresh new container from a docker image. However, it doesn’t run it immediately.

- docker container run -dt {container-name}
  </br>Run command is a combination of create and start as it creates a new container and starts it immediately. In fact, the docker run command can even pull an image from Docker Hub if it doesn’t find the mentioned image on your system.

- docker container run -d {container-name} {command}
  </br>Used to *Overide* default container command

- docker system events
  </br>To get event from the docker container.
  </br>docker system events --since {date}
  </br>To get events from this particular date
  </br>docker system events --since 2022-02-03

- docker system df
  </br>Gives space of each images, containers, local volume & cache

- docker system df -v
  </br>Gives per component level size

- docker container run -dt --name testcontainer busybox ping -c10 google.com
  </br>This is a container operation with detachable tag name of testcontainer on image of busybox and count of 10 ping on google.

- docker container run -dt -rm --name testcontainer busybox ping -c10 google.com
  </br>Adding **rm** option on starting to remove the container on being executed

- docker container commit {CONTAINER_ID}/{image-name} {new image-name}
  </br>To commit a container with made changes
  </br>Example: docker container commit --change='CMD' ["ash"]' busybox

- docker build -t --name {name} . {specify the directory}
  </br>New image is build with the changes and the image created will be stored in docker

- docker run -dt --name tmp --health-cmd "curl -f <http://localhost>" busybox
  </br>docker run -dt --name tmp --health-cmd "curl -f <http://localhost>" --health-interval=5s busybox
  </br>docker run -dt --name tmp2 --health-cmd "curl -f <http://localhost>" --health-interval=5s --health-retries=1 busybox
  </br>Used to check health of container.

- docker container run -dt --name base01 base01 -c10 google.com
  </br>The commands is executed after making bin/ping as ENTRYPOINT for the program.

- docker rmi {image-name}/{image-id}
  </br>To remove Images from docker

- docker tag {image-id} name:{tag}
  </br>Creates alias for the image if the image already exist else names the *dangling* image.

- docker image history nginx
  </br>To view the layers of nginx

- docker image inspect nginx --format='{{.Id}}'
  </br>To inspect the image and takeinformation from the json outcome.To get outcome as json we use the following command
  </br>docker image inspect {name} --format='{{json .Id}}'

- docker image prune
  </br>Deletes the dangling images if no container of it is running or is present.

- docker image prune -a
  </br>Deletes all images if no container of it is running or is present.

- docker export myubuntu > myubuntu.tar
  </br>Export the image to tar file
  cat myubuntu.tar | docker import - myububtu:latest
  </br>Import image from tar file
  </br>Exporting and importing the image file flattens the file and sometimes reduces space.

- docker run -d -p 5000:5000 --name registry registry:2
  </br>Download and run registry
  </br>docker tag ubuntu:latest localhost:5000/myubuntu
  </br>docker push localhost:5000/myubuntu
  </br>docker pull localhost:5000/myubuntu
  </br>This is how docker registry is used.

- docker tag busybox singhpriansh/dock_hub:v1
  </br>Tag busybox image so as it remains uneffected on operations on the image
  </br>docker push singhpriansh/dock_hub:v1
  </br>Push image to dockers repository
  </br>docker pull singhpriansh/dock_hub:v1
  </br>Pull image from docker repository
  </br>This is how docker hub is used.

- docker search {image-name}
  </br>To search for image using cli
  </br>docker search nginx --limit {N}
  </br>To limit the search results
  </br>docker search nginx --filter "is-official=true"
  </br>Using filter we can put various parameters to search from

- docker save myapp > myapp.tar
  </br>docker load < myapp.tar
  </br>To create/save and load a image across devices

- docker build -t without-cache .
  </br>Build docker without cache
  </br>docker build -t with-cache .
  </br>Build docker with cache this fastens the process of image making from Dockerfile

- docker network ls
  </br>Shows available network drivers available

- docker network inspect {network}
  </br>Shows information regarding particular network driver

- docker container run -dt --name myhost --network host ubuntu
  </br>To launch a container in the given network

- docker network create --driver bridge mybridge
 </br>Creates a new bridge network

- docker network create --opt encrypted --driver overlay {my-secure-network}
  </br>To secure an overlay network we use --opt encrypted flag

- docker container run -dt --name container1 busybox sh
  </br>docker container run -dt --link container1:container --name container2 busybox sh
  </br>This is legacy approach in which the container1 is resolved in the environment of container2 which can be detected by ping operation.

- docker service ls
  </br>Lists all the services

- docker service ps {service name}
  </br>Information related to the service and the node in which the service is running

- docker service rm {service name}
  </br>We directly rm the service when not needed

- docker service scale webserver={N}
  </br>We can specify multiple services in the same command.
  </br>docker service update --replicas N webserver
  </br>Tasks will be scaled to N

- docker service create --name webserver --replicas 1 nginx
  </br>To create a service of websrever with one replica

- docker service create --name antivirus --mode global -dt ubuntu
  </br>A service of anitvirus is created and run on every node

- docker service inspect {servie name}/{id}
 </br>Procides detail about the service
 </br>docker service inspect {service name}/{id} --pretty
 </br>Provides readable output for the services

- docker service create --name mywebserver --replicas 2 --publish 8080:80 nginx
  </br>Service is created with name mywebserver replicas of 2 and published on port 8080 of host from 80 of container on the image of nginx.

- docker node ls
  </br>Shows all the nodes

- docker node update --availability drain swarm2
  </br>This drains the swarm2 node. All the container are moved from this node making it free for maintenance

- docker node update --availability active swarm2
  </br>This brings back the node to active state and maintenance

- docker node inspect {name}/{id}
  </br>Provide detail about the node
  </br>docker node inspect {name}/{id} --pretty
  </br>Provides readable output for the node

- docker compose up -d
  </br>We can start all the services with single command in detached mode
  </br>docker-compose down
  </br>We can stop all the services with single cammand

- docker compose config
  </br>Shows if the format of the docker-compose yml file is correct

- docker stack deploy --compose-file docker-compose.yml mydemo
  </br>To deploy the services which are a part of docker services in yml file across swarm cluster

- docker stack ps {name of the container}
  </br>Provides information regarding services in swarm.

- docker stack rm mydemo
  </br>Container which are part of stack will be removed.

- docker swarm update --autolock=true
  </br>To turn on lock on swarm
  </br>A new password will be generated which will be required to unlock the swarm

- systemctl restart docker
  </br>We need to restart docker for lock to take effect.
  </br>This command varies from system to system

- docker swarm init
  </br>To initialise swarm with the node acting as manager.

- docker swarm init --advertise-addr {ip}
 </br>To add other nodes to the client given.

- docker swarm join-token manager
  </br>To add a manger node to this swarm node we get the command using this command.

- docker swarm unlock
  </br>Requires key generated in last step

- docker swarm unlock-key --rotate
  </br>Used to rotate the key

- docker service create --name myservice  --mount type=colume,source=myvolume,target=/mypath nginx
  </br>Creates volumes in one of the swarm server

- docker service create --name myconstraint --constraint node.labels.region==blr replicas 3 nginx
  </br>It will create service based constraints which in name labels region of 'Bangalore' and replicas of 3.

- docker node update --label-add region=mumbai {name}/{id}
  </br>To add label to a specific node

- docker service create --name myoverlay --network --replicas 3 nginx
  </br>When we define network with service it gets propageted to other nodes as well.

- docker service create-name demoservice --hostname="{{.Node.Hostname}}-{{.Service.Name}}" nginx
  </br>We use placeholder template by two curly braces.

### Command strings

Abbreviation | Complete string  |
-------------|------------------|
 -a  | --all
 -p  | --port / --publish
 -P  |  (publish all)
 -d  | --detached
 -a  | --attached
 -i  | --interactive
 -t  | --tty / --tag
 -e  | --env

### Docker cli

- Docker cli can be used to manage vaious aspects related to Docker Images which includes building, removing, saving, tagging and others.

## Docker restart policies

- By default, Docker container will not start when they exit or when docker daemon is restarted. Docker provides restart policies whether your container start automatically when they exit, or when Docker reastarts.
- We can specify the restart policy by using the --restart flag with docker run command.

Flag           |     Desciption        |
---------------|-----------------------|
no             | Do not automatically restart the container (the defalut) |
on-failure     | Restart the container if it exits due to an error, which manifests as a non-zero exit code |
unless-stopped | Restart the container unless explicitly stopped or Docker itslef is stopped or restarted |
always         | Always restart the container if it stops |

## Dockerfiles

- A **Dockerfile** is a text document that contain all the commands a user could call on the command line to assemble an image.

- Sample content of docker file
  
  ```[]
  FROM ubuntu
  RUN apt-get update
  RUN apt-get install nginx -y
  CMD ["nginx", "-g", "daemon off"]
  ```

- ### Commands

  - FROM : Build the docker image with specific command
  - RUN : run the specific instruction
  - CMD : start the container with specified command but commands can be overridden.
  - COPY : takes in a src and destination.  It only copy in a local file or directory from your host.
  - ADD : lets you do two additional operations
    - use a URL instead of a local file / directory.
    - extract a tar file from the source directory into the destination.

    Using ADD to fetch package from remote URLs is strongly discouraged, instead use **curl** or **wget**.
  - EXPOSE : informs Docker that the container listens on the specified network ports at runtime without actually publishing the port.
  
    It *functions as a type of documentation* between the person who build the image and the person who runs the continer, about which ports are intended to be published.
  - HEALTHCHECK : allows us to tell the platform on how to test that our application is healthy.
  </br>That's basic check and does not tell the detail about the application.
    - --interval = DURATION(default:30s)
    - --timeout = DURATION(default:30s)
    - --start-period = DURATION(default:0s)
    - --retries = N(default:3)
  </br>Exit Status
    - 0: Success = the containeris healthy and ready for use
    - 1: Failure = the container is not working correctly
    - 2: Reserved = do not use this exit code
  - ENTRYPOINT : best used to set the image's main command and doesn't allow to override the command.
    </br>Example :ENTRYPOINT ["bin/ping"]
  - WORKDIR : instruction sets the working directory for any RUN, CMD, ENTRYPOINT,COPY and ADD instruction that follow it in the Dockerfile
    </br>Example :WORKDIR /file
  - ENV : instruction sets the environment variable {key} to the value {value}.
    </br>Example :ENV app value, $app => value

- When changes are made inside the container, it can be useful to commit a container's file changes into a new image.
  - By default the container being commited and its processes will be paused while the image is commited.

## Docker Layers

- A docker image is built up from a series of layers.
- Each layer reperesent an instruction in the image's Dockerfile.
- The major difference between a container and an image is the top writable layer.
- All writes to the container that add new or modify existing data are stored in this writable layer.
- docker container history {name} is used to get layers of the image.

## Docker Images

- A docker image contains lots of imformation, some of these include:
  - Creation date
  - Command
  - Environment variables
  - Architecture
  - OS
  - Size
- **docker image inspect** command allows us to see all the information associated with a docker image.
- **docker image prune** command allows us to clean up unused images. By default, command will only clean up dangling images.
- *Dangling Images* = Images without Tags and not referenced by any container.
- Modify Image to Single Layer : In a generic scenerio, the more the layers an images has, the more the size of the image.*Flattening* an image to single layer can help reduce the overall size of the image.
- Docker Registry : A Registry is stateless, highly scalable server side application that stores and lets us distribute Docker images.
</br>There are various types of registry available, which includes
  - Docker Registry
  - Docker Truster Registry
  - Private Repository (AWS ECR)
  - Docker Hub

- Docker creates container images using layers. Each command that is found in a Dockerfile creates a new layer.
</br>Docker uses a layer cache to optimize the process of building Docker images and make it faster. If the cache can't be used for a particular layer, all subsequent layers won't be loaded from the cache.
</br>docker build -t with-cache . is used to make image with cache

## Docker Networking

- Docker networking subsystem is pluggable, using drivers.
- There are several drivers available by default, and provides core networking functionality.
  - bridge
  - host
  - overlay
  - macvlan
  - none

```[]
  +-----------------+                 +-----------------+
  | 172.17.0.0/16   |                 | 192.168.0.0/16  |
  | +-------------+ |                 | +-------------+ |
  | | Container 1 |<|----172.17.0.2   | | Container 1 | |
  | +-------------+ |                 | +-------------+ |
  | +-------------+ |                 | +-------------+ |
  | | Container 2 |<|----172.17.0.3   | | Container 2 | |
  | +-------------+ |                 | +-------------+ |
  +-----------------+                 +-----------------+
    Bridge Network                      Custom Network
```

### Bridge Network
  
- A bridge network uses a software bridge while allows containers connected to the same bridge network to communicate, while providing isolation from container which are not connected to that bridge network.

  ```[]
  +-----------------------------------------------------+
  |  |      C1     |  |      C2     |  |     C3      |  |
  |  | 172.17.0.18 |  | 172.17.0.19 |  | 172.17.0.20 |  |
  |  +-------------+  +-------------+  +-------------+  |
  |          eth0             eth0             eth0     |
  |      +---------------------------------------+      |
  |      |              172.17.0.1               |      |
  |      |           Docker0 bridge              |      |
  |      +------------------|--------------------+      |
  |              +----------|----------+                |
  |              |    iptables / NAT   |                |
  +--------------+----------|----------+----------------+
              192.168.50.16 | eth0
  ```

  Bridge is the default driver for Docker.If we don't specify a driver, this is the type of network you are creating. A newly-started container connect to it unless otherwise specified.</br>
  User-Defined Bridge Network are superior to the default bridge network.

#### User-Defined bridge Network

- User-defined bridge provide better isolation and interoperability between containerized applications.
- User-defined bridge provide automatic DNS resolution between containers.
- Containers can be attached and detached from user-defined networks on the fly.
- Each user-defined network creates a configurable bridge.
- Linked containeron the default bridge network share environment variables.

### Host Network

- This driver removes the network isolation between host and the docker containers to use host's network directly.
- For instance, if we run a container which binds to port 80 and we use host networking, the container's application will be available on port 80 on the host's IP address.

### None Network

- If we want to completely disable the network stack on a container. we can use the none network.
- This mode will not configure any IP for the container and doesnot have any access to the external network as well as for other containers.

### Overlay Network

- The overlay network driver creates a distributed network among multiple Docker daemon hosts.
- Allows container connected toit to communicate securely.
- For overlay networks, the container can be spreaded across multiple servers
- If the container are communicating with each other, it is recommanded to secure communication.
- To enable encryption, when we create an overlay netkork, we pass the --opt encrypted flag

## Container Orchestration

- Container Orchestration is all about managing the life cycles of container, especially large, dynamic environments.

  ```[]
  +------------+  +------------+ +------------+
  | Web Server |  | Web Server | |            |
  |            |  |            | |            |
  | App Server |  | App Server | |            |
  +------------+  +------------+ +------------+
       VM 1            VM 2          VM 3
  ```

- Importance of Container Orchestration
  </br>Container Orchestration can be used to perform lots of tasks, some of them includes:
  - Provisioning and deployment of containers
  - Scaling up or removing container to spread load evenly
  - Movement of containers from one host to another if there is a shortage of resources
  - Load balancing of service discovery between container
  - Health monitoring of containers and hosts

- There are many container orchestration solutions available, some of the popular once iclude :
  - Docker Swarm
  - Kubernetes
  - Apache Mesos
  - Elastic Container Service (AWS ECS)
  </br>There are also various container orchestration platforms available like EKS.

### Docker Swarm

- Docker Swarm is a container orchestration tool which is natively supported by Docker.
- Lab setup:
  
  ```[]
                [ +---------+  +---------+ +---------+  ]
  Swarm Cluster { | Node 01 |  | Node 02 | | Node 03 |  }
                [ +---------+  +---------+ +---------+  ]
  ```

- Initializing Docker Swarm
  - A *node* is an instance of the Docker engine participating in the swarm.
  - To deploy your application to a swarm, you submit a service definition to a *manager node*.
  - The manager node dispatches units of work called tasks to *worker nodes*.
  1. Manager Node Command:
  </br>docker swarm init -advertise-addr \<MANAGER-IP>
  2. Worker Nodes Command:
  </br>docker swarm join-token worker

```[]
                              task      container
                            +---|-----------|-----------+
         service            | nginx 1 ( nginx: latest ) |
  . . . . .|. . . . .     / +---------------------------+
  . +------|------+ .   /         available node
  . |      |      | . /     +---------------------------+
  . |   3 nginx   | . ----> | nginx 2 ( nginx: latest ) |
  . |  replicas   | . \     +---------------------------+
  . +-------------+ .   \          available node
  .  swarm manager  .     \ +---------------------------+
  . . . . . . . . . .       | nginx 3 ( nginx: latest ) |
                            +---------------------------+
                                  available node
```

#### Service

- A service is the definition of the tasks to execute on the manager or worker nodes.
</br>Create service command
</br>docker service create --name webserver --replicas 1 nginx

- Once we have deployed a service to a swarm, we are ready to use the Docker CLI to scale the number of container in the service.
- Container running in a service are called "tasks"
- There are two ways in which we can scale serivce in swarm:
  - docker serivce scale webserver=5
  - docker service update --replicas 5 webserver

- There are two types of services deployments, replicated and global

  - **Replicated Services :** For a replicated service, we specify the number of identical tasks we want to run. Example : we decide to deploy a NGINX service with two replicas, each serving the same content.
  - **Global Service :** A global service that runs one task on every node.
  Each time you add a node to the swarm, the orchestrator creates a task and the scheduler assigns the task to the new node.

#### Docker Inspect

- Docker Inspect provides detailed information of the Docker Objects.
  </br>Some of these Docker Object includes:
  - Docker Container
  - Docker Network
  - Docker Volumes
  - Docker Swarm Services
  - Docker Swarm Nodes

#### Docker Compose

- Compose is a tool for defining and running multi-container Docker applications.
- With compose, we can use a YAML file to configure application services.
- We can start all the sevices with single command.
  - docker-compose up
- We can stop all the services with single cammand.
  - docker-compose down
- Sample content of Docker compose directory
  - Directory
    - docker-compose.yml

  ```[]
  services:
    webserver:
      image: nginx
      ports:
        - "8080:80"
    database:
      image: redis
  version: '3.0'
  ```

#### Multi-Service Apps

- A specific web-application might have multiple containers that are require as part of the build process.
- Whenever we make use of docker service, it is typically for a single container image.
- The docker stack can be used to manage a muilti-service application.
- **Docker Stack**
  - A stack is a group of interrelated services that share dependencies, and can be orchestrated and scaled together.
  - A stack can compose **YAML** file like one we define in Docker Compose.
  - We can define everything within the YAML file that we might define while creating a Docker Service.

#### Locking Swarm Cluster

- Swarm Cluster contains lot of sensitive information, which includes :
  - TLS key used to encrypt communication among swarm node.
  - Krys used to encrypt and decrypt the Raft logs on disk
- If our Swarm is compromised and if data is stored in plain-text, an attack can get all the sensitive information
- Docker Lock allows us to have control over the keys.
- Location of swarm certificate
  </br>/var/lib/docker/swarm/certificates
- Getting swarm-key
  </br>cat swarm-node.key

#### Service deployment

- A service may be configured in such a way that no node currently in the swarm can run its tasks.
- In this case, the service remains in state pending
- There are multiple reason why a service might go into pending state.
- Examples :
  - If all nodes are drained, and we create a service, it's pending until a node becomes available.
  - We can reserve a certain amount of memory for a service. If no node in the swarm has the required amount of memmory, the service remains in a panding state until a node is available which can run its tasks.
  - We have imposed a certain kind of placement constraints.

#### Control service Placement

- Swarm services provide a few different ways for us to control scale and placement of services on different nodes.
  - Replicated and Global Service
  - Resource Constraints [requirement of CPU and Memory]
  - Placement Constraints [only run on nodes with label pci_compliance=true]
  - Placment Preferences

#### Custom overlay network for swarm

- We secure the networks using --opt encrypted flag in the create command used to create service.
- When we enable overlay encryption, Docker creates IPSEC tunnels between all the nodes where tasks are scheduled for services attached to the overlay network.
- These tunnels also use the AES algorithm in GCM mode and manager nodes automatically rotate the keys every 12 hours.
Overlay network encrytion is not supported on Windows. If a windows node attempts to connect to an encrypted overlay network, no error is detected but the node will not be able to communicate.

#### Creating Services using Template

- We can make use of templates while running the service create command in swarm
- Example: docker service create-name demoservice --hostname="{{.Node.Hostname}}-{{.Service.Name}}" nginx
- There are three supported flags for the placeholder templates:
  - --hostname
  - --mount
  - --env

- Valid Placeholders
  Placeholder      | Description
  -----------------|--------------
  .Service.ID      | Service ID
  .Service.Name    | Service name
  .Service.Labels  | Service labels
  .Node.ID         | Node ID
  .Node.Hostname   | Node Hostname
  .Task.ID         | Task ID
  .Task.Name       | Task name
  .Task.Slot       | Task slot

#### Split Brain

- Split-brain is the idea that a cluster can have communication failures, which can cause it to split into subclusters. Fencing is the way of ensuring that one can safely proceed in these cases, and quorum is the idea of determining which subcluster can fence the others and proceed to recover the cluster services.

#### Importance of Quorum

- We should maintain an odd number of nodes within the cluster.
  Cluster Size | Majority | Fault Tolerance
    1          |  0       |   0
    2          |  2       |   0
    3          |  2       |   1
    4          |  3       |   1
    5          |  3       |   2
    6          |  4       |   2
    7          |  4       |   3

#### High availability of swarm manager nodes

- Manager Nodes are responsible for handling tasks such as :
  - maintaining cluster state
  - Scheduling services
  - Serving swarm node HTTP API endpoints

- Using a Raft implementation, the managers maintain a consistent internal state of the entire swarm and all the services running on it.
- Swarm comes with it's own fault tolerance features.
- Docker recommends implement an odd number of nodes according to organisation's high-availability requirements.
- An N manager cluster tolerates the loss of at most (N-1)/2 managers.

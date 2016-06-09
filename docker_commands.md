# Welcome to the World of Docker Commands

------

## Docker Installation Commands

### Install the latest version of Docker with apt-get
sudo apt-get upgrade docker-engine

------

## Install Docker on Ubuntu (Way 1)

### 1. Log into your Ubuntu installation as a user with sudo privileges.

### 2. Update your APT package index.
sudo apt-get update

### 3. Install Dokcer
sudo apt-get install docker-engine

### 4. Start the Docker daemon
sudo service docker start

### 5. Verify Dokcer is installed correctly
sudo docker run hello-world
This command downloads a test image and runs it in a container. When the container runs, it prints an informational message. Then, it exits.

------

## Install Docker on Ubutntu by command line (Way 2)

### 1. Search docker.io
apt-cache search docker.io

### 2. Show docker.io
apt-cache show docker.io

### 3. get wget command from https://get.docker.com
'wget -qO- https://get.docker.com/ | sh' // pipe the file to the shell

### 4. In order to simplify using Docker, you can get non-sudo access to the Docker socket by adding your user to the docker group, then logging out and back in again:
sudo usermod -aG docker your-user // sudo usermod -aG docker jun, do anything with Docker root priviledges

docker info // see a bunch of info about your Docker installation
### 5. verify the groups that user jun has
id jun // checks the groups that user jun has

### 6. Docker hub and Docker registry url
hub.docker.com
registry.hub.docker.com

### 7. Look for Docker images
docker search mysql
docker search ubuntu // will get the latest Ubuntu same as docker search ubuntu:latest
docker search ubuntu:14.04 // will get the version of Ubuntu matches the tag 14.04

### 8. Pull Docker images
docker pull ubuntu:14.04
docker pull ubuntu:latest // same as docker pull ubuntu, as it gets the latest version by default

### 9. Show all Dokcer images locally
docker images // shows a list of Docker images downloaded
docker images -a
docker images -aq

------

## Docker Operation Commands

### 1. List all Docker Containers
#### List all running containers
docker ps

#### List containers both running and not running
docker ps -l

docker ps -a 
docker ps -aq

### 2. Remove old Docker containers 
docker rm `docker ps --no-trunc -aq`
 or
docker rm `docker ps -a -q`
 or
docker rm $(docker ps -aq)

### 3. Remove single or more Dokcer containers
docker rm <CONTAINER ID|NAME> <CONTAINER ID|NAME>

### 4. Remove all Docker images
docker rmi $(docker images -q)

### 5. Remove single Docker image
docker rmi the_image_id

### 6. List all Dokcer images
docker images -aq 
 or
docker images -q

### 7. Create Docker Containers. 
####Every Dokcer image has to start with a base layer. Common base layers are Ubuntu and CentOS, Debian (the smallest of these three). If you don'thave the image locally, Docker will downloaded it first. To create a new container, you need to use a base image and specify a command to run.
####. -t: pseduo-tty,  -i: interactive --name: name_tag for the container, -d: dettach mode /bin/bash: starts a bin/bash terminal in the container. When you "run" any process using an image, in return, you will have a container. When the process is not actively running, this container will be a non-running container. 

docker run -i -t ubuntu:14.04 /bin/bash  // -i means interactive, keep standard input open -t means tty, allocate a pseduo-tty /bin/bash means use the bash shell and get inside the container

docker run -it ubuntu:14.04 /bin/bash // -i -t or -ti or -it, let you interact with the container via command line

docker run -it --name my-ubuntu ubuntu /bin/bash

docker run --name juns-ubuntu -it ubuntu:14.04 bash    // the container will be started in a bash terminal

docker run -it --name duck -d ubuntu /bin/bash // strat a container with name "duck", -d means in "detach mode"


# OSX/Windows users will want to remove --­­user "$(id -­u):$(id -­g)"
docker run -it --rm --user "$(id -u):$(id -g)" \
  -v "$PWD":/usr/src/app -w /usr/src/app rails:4 rails new --skip-bundle dummy
The -v "$PWD":/usr/src/app -w /usr/src/app segment connects our local working directory with the /usr/src/app path within the Docker image. This is what allows the container to write the Rails scaffolding to our work station.



### 8. Install software on your container. Ubuntu image is very light-weight, a bare-boned image. An important strategy of creating Docker images is keeping them as light as possible. Let's install wget:
apt-get update
apt-get install wget

### 9. top to see all process
top

### 10. Exiting a Docker container without messing its read/write changes and provide you host system console. This will leave it running in the backgorund. When you can go back to it and the container state is left as is/untouched
CTRL + P + Q

### 11. List the top process that's running
ps aux | grep top  // list the top process that's running as we've only run top inside the docker container

ps -aux | grep top 


### 12. List all Docker containers running/stopped 
docker ps
docker ps - a  //list all docker containers with conatiner id/name, created/up time
docker ps -a -q
docker ps -aq

### 13. Go back to the Docker container you left running by typing CTRL + P + Q, by attaching back to it
 docker attach <CONTAINER ID|NAME>

 docker attach docker_container_name // as you specified using docker run --name xxx -it ubuntu /bin/bash

docker attach tender_shirley

docker attach d531228eaa3d  

### 14. Commit your Docker container as an image for shipment
docker commit -m "Juns ubuntu with Redis installation" -a "Your Name" container_tag_name docker_hub_username/container_name_tag:container_version

docker commit -m "Ubuntu with Redis" -a "Jun Zheng" my-redis jzheng/my-redis:latest

#### This command compiles our container’s changes into an image. -m specifies a commit message, and -a let’s us specify an author. jzheng/my-redis:latest is formatted author/name:version. Author refers to your username on Docker Hub. If you don’t want to push your image to the Docker Hub, then this doesn’t matter, and you can use anything you want. If you do, you will need to create an account and use docker push to push the image upstream.

#### Docker commit creates an image containing the changes we made to the original Ubuntu image. This makes distributing Docker containers super fast since people won’t have to re-download layers (such as Ubuntu:latest) that they already have. In a container, every time you run a command, add a file or directory, create an environmental variable, etc. a new layer is created. Docker commit groups these layers into an image. When distributing Docker images, you should carefully optimize your layers to keep them as small as possible. 

### 15. Exit Docker container/ stop Docker container, all the changes made on the read/write layer will be lost, but the container itself is intact. This will stop the current container.
CTRL + D // with this command, when you docker attach container_id to go back to the container, all the read/write changes are lost, but the container is intact.

### 16. Start and Stop Docker Containers. Docker run creates the container, we'll need to run docker start container_name/container_id if the conatiner has been stoped by doing: docker stop container_id/container_name

docker start <CONTAINER ID|NAME>

docker start tender_shirley // this starts the container in the background

docker top tender_shirley // see what processes are running in the container tender_shirley

docker stop <CONTAINER ID|NAME>

docker stop tender_shirley // stop the container tender_shirley

### 17. Persistant Storage for Docker Container. Docker's writable layer is not persistant, once we exit the container, the data will be lost, we'll need to add volume to the container to achieve persistant data storage. 
#### Give a volume to a container -v/data (-v add volume, give it a mount point) and it's data will be persistent. You'll find a data directory in the root, go inside and create some files, if you exit CTRL + D, the files will be saved, not lost.

docker run -it -v /data --name=goose ubuntu /bin/bash  // -v add volume, give it a mount point -v/data

####. You can also use directory from your host machine as volumes and attach it with docker container. Attaches the /Users/dev/Documents/dev/docker folder to the data folder in the Docker container 'sheep', whatever you save inside the data folder appears in the dev/docker folder on the host machine of docker server.
docker run -it -v /Users/dev/Documents/dev/docker:/data --name=sheep ubuntu /bin/bash

### 18. Docker Container with Network Connection
####. Expose a port/open up a port in a Docker container, so the container will be able to commuicate to the world through this port, -p 3306: exposes port 3306 for the container
docker run -it -d -p 3306 mysql  /bin/bash // -d run in detach mode, -p give it port 3306 which is the default mysql port

iptables -L -t nat // -t means table; nat: network table translation; if you do this command, you'll see the iptables in which you can find the port 3306 for mysql

docker ps // shows the following details:

CONTAINER ID  IMAGE  COMMAND          CREATED      STATUS               PORTS                     NAMES
00450cb79f00  mysql  entrypoint.sh /bin/" 11 minutes ago Up 11 minutes 0.0.0.0:32770->3306/tcp   clever_euclid

Here, 0.0.0.0:32770->3306/tcp // this line means that the localhost port:32770 is forwarded to the mysql container port 3306 (192.168.99.100:3306), but the outside computer cannot reach the mysql container port 3306, so we'll need to forward the localhost port:32770 to the mysql container port 3306. But in reality, we want to forward localhost:3306 to docker container port:3306.

####. Create a Docker MySQL container forward localhost:3306 to docker container port:3306

docker stop cleve_euclid // now we stop the mysql container named cleve_euclid

docker run -d -p 3306:3306 -it mysql /bin/bash // run a Docker mysql container in detach mode, forward localhost:3306 to mysql docker container port 3306

docker ps // shows that the localhost:3306 is forwarded to mysql container port:3306

CONTAINER ID  IMAGE  COMMAND      CREATED      STATUS               PORTS            NAMES
2d1a153b99d6   mysql "/entrypoint.sh /bin/"  7 seconds ago  Up 6 seconds  0.0.0.0:3306->3306/tcp   backstabbing_borg

ip addr show // list all IP addresses

get IP address of a Docker container
docker inspect --format '{{ .NetworkSettings.IPAddress }}' docker_container_id or docker_container_name
docker inspect --format '{{ .NetworkSettings.IPAddress }}' duck

#### We can also open up a specific IP address and port connection to the Docker conatiner
docker run -d -p 192.168.56.101:3306:3306 -it --name=cat mysql /bin/bash
forward 192.168.56.101:3306 to docker mysql image named cat's port:3306

docker ps

docker attach cat

ip addr show // the (host machine ip addr show) has a docker bridge that forwards connection to the docker container's port

### 19. Use Dokcerfile to create a Docker iamge.
####. A Dockerfile is a set of instructions written as a shell script for creating a Docker image. Below is an example Dockerfile that creates a Redis image on a Ubuntu layer.
Dokcerfile
------
```
############################################################
# Dockerfile to build Redis container images
# Based on Ubuntu
############################################################

FROM ubuntu:latest
MAINTAINER junzheng
RUN echo 'Hello Docker!.'
RUN echo 'RUN command is used to build the image/forming another layer on top of the previous one which is commited'
RUN echo 'Now updating apt-get application repository list'
RUN apt-get update
RUN echo 'installing wget'
RUN apt-get install -y wget
RUN echo 'installing build-essential'
RUN apt-get install -y build-essential tcl8.5
RUN echo 'downloading redis'
RUN wget http://download.redis.io/releases/redis-stable.tar.gz
RUN echo 'unzipping redis'
RUN tar xzf redis-stable.tar.gz
RUN echo 'make and install redis'
RUN cd redis-stable && make && make install
RUN ./redis-stable/utils/install_server.sh
EXPOSE 6379
RUN echo 'Port 6379 exposed for redis'
ENTRYPOINT  ["redis-server"]
RUN echo 'Redis-server running at port 6379'

CMD 'echo' 'Redis container is instantiated.'
```
------
There are some special things in this Dockerfile. FROM tells Docker which image to start from. As you can see, we are starting with Ubuntu. RUN simply runs a shell command. EXPOSE opens up a port to be publically accessible. 6379 is the standard Redis port. ENTRYPOINT designates the command or application to be run when a container is created. In this case whenever a container is created from our image, redis-server will be run.

#### Dockerfile example for bulding a MongoDB image
------
```
############################################################
# Dockerfile to build MongoDB container images
# Based on Ubuntu
############################################################

# Set the base image to Ubuntu
FROM ubuntu

# File Author / Maintainer
MAINTAINER Example McAuthor

# Update the repository sources list
RUN apt-get update

################## BEGIN INSTALLATION ######################
# Install MongoDB Following the Instructions at MongoDB Docs
# Ref: http://docs.mongodb.org/manual/tutorial/install-mongodb-on-ubuntu/

# Add the package verification key
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10

# Add MongoDB to the repository sources list
RUN echo 'deb http://downloads-distro.mongodb.org/repo/ubuntu-upstart dist 10gen' | tee /etc/apt/sources.list.d/mongodb.list

# Update the repository sources list once more
RUN apt-get update

# Install MongoDB package (.deb)
RUN apt-get install -y mongodb-10gen

# Create the default data directory
RUN mkdir -p /data/db

##################### INSTALLATION END #####################

# Expose the default port
EXPOSE 27017

# Default port to execute the entrypoint (MongoDB)
CMD ["--port 27017"]

# Set default container command
ENTRYPOINT usr/bin/mongod
```
------
### 20. Build an image from Dockerfile
#### Build an image using the Dockerfile at current location. The -t [name] flag here is used to tag the image. To learn more about what else you can do during build, run sudo docker build --help. When a Dockerfile is finished executing, you end up having formed an image, which then you use to start (i.e. create) a new container.
docker build -t my_new_redis_image .    // docker build 
This command will create an image tagged redis from your Dockerfile.

Finally, let’s create a running container from our image. Run the following command:
docker run -d -p 6379:6379 redis

sudo docker build -t my_mongodb .  // building a MongodDB image with tag name my_mongodb at the current directory

sudo docker run --name my_first_mdb_instance  -it my_mongodb // running a MongoDB container/instance with the image we have built.

Note: If a name is not set, we will need to deal with complex, alphanumeric IDs which can be obtained by listing all the containers using sudo docker ps -l.

docker ps -l

Note: To detach yourself from the container, use the escape sequence CTRL+P followed by CTRL+Q. (CTRL + P + Q)
CTRL + P + Q

docker attach my_first_mdb_instance

###21. Remove Dangling/Orphaned Docker Volumes
$ docker volume ls -qf dangling=true

Eliminate all of them with

$ docker volume rm $(docker volume ls -qf dangling=true)

### 22. Run Bash Commands with Docker Container

$ docker run --rm -v $PWD:$PWD -w $PWD -u=$(id -u) <container name> bash -c 'whoami'


### 23. Default jekyll server volume :/srv/jekyll

docker run --rm --label=jekyll --volume=$(pwd):/srv/jekyll -it -p 127.0.0.1:4000:4000 jekyll/jekyll

docker run --rm --label=jekyll --volume=$(pwd):/srv/jekyll -it -p 127.0.0.1:4000:4000 jekyll/jekyll




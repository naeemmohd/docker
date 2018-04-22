##### Step 1 : Installation of pre-requisite packages
> yum install -y yum-utils device-mapper-persistent-data lvm2

##### Step 2 : Setting up Docker yum repository and install docker
> yum-config-manager –add-repo https://download.docker.com/linux/centos/docker-ce.repo
> yum -y install docker-ce

##### Step 3 : Start Docker
> systemctl start docker
> systemctl enable docker

##### Step 4 : Run Hello world to test docker installation
> docker run hello-world

##### Some basic docker commands
docker --help

##### Command to check docker version(basic info)
> docker --version

##### Command to check docker version(detailed info)
> docker version

##### To check docker info(detailed docker metadata info) 
> docker info

##### To pull an image from Docker Hub(latest tag)
> docker pull centos

##### To pull an image from Docker Hub(specific tag)
> docker pull centos:7

##### To check the docker images
> docker images

##### to run a docker image(in backgrounf mode)
> docker run -d centos bash

##### to run a docker image(in backgrounf mode)
> docker run -it centos bash

##### list containers( all  running as well as exited)
> docker container ls
> docker ps -a

##### list containers ids( all  running as well as exited - use option -q)
> docker container ls -q
> docker ps -a -q

##### filter containers – docker container ls -a filter <filtercondition>
> docker container ls -a filter “excited=0”
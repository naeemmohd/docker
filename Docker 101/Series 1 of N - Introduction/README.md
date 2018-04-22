### Step 1 : Installation of pre-requisite packages
  ```
  yum install -y yum-utils device-mapper-persistent-data lvm2
  ```
  
### Step 2 : Setting up Docker yum repository and install docker
  ```
  yum-config-manager –add-repo https://download.docker.com/linux/centos/docker-ce.repo 
  yum -y install docker-ce
  ```
### Step 3 : Start Docker
  ```
  systemctl start docker
  systemctl enable docker
  ```

### Step 4 : Run Hello world to test docker installation
  ```
  docker run hello-world
  ```
  
### Some basic docker commands
  ```
  docker --help
  ```
  
### Command to check docker version(basic info)
  ```
  docker --version
  ```
  
### Command to check docker version(detailed info)
  ```
  docker version
  ```
  
### To check docker info(detailed docker metadata info) 
  ```
  docker info
  ```
  
### To pull an image from Docker Hub(latest tag)
  ```
  docker pull centos
  ```
  
### To pull an image from Docker Hub(specific tag)
  ```
  docker pull centos:7
  ```
  
### To check the docker images
  ```
  docker images
  ```
  
### To run a docker image(in backgrounf mode)
  ```
  docker run -d centos bash
  ```
  
### To run a docker image(in backgrounf mode)
  ```
  docker run -it centos bash
  ```
  
### To list containers(all  running as well as exited)
  ```
  docker container ls
  docker ps -a
  ```
  
### To list containers ids(all  running as well as exited - use option -q)
  ```
  docker container ls -q && docker ps -a -q
  ```
  
### To filter containers – docker container ls -a filter <filtercondition 
  ```
  docker container ls -a filter “excited=0”
  ```
  
### Special Note to setup t GitHub user name and email to local git
  ```
  git config --local user.email "naeem.mohd@hotmail.com" && git config --local user.name "Mohd Naeem"
  ```
  
### Remove all images and all containers
  ```
  docker rmi $(docker images -q) 
  docker rm $(docker ps -a -q)
  ```
### Login to docker hub to push or pull images ( use your DockerHub login user and password)
  ```
  docker login 
  ```  
  
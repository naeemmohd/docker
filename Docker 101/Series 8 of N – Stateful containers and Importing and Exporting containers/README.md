### Stateless vs Stateful containers
 - Stateless - they don't need to maintain the state of an application
    - e.g The TicTacToe game container we created is a simple game. We just wanted that when the container image is downloaded then the game should run. But we are not maintaining any users, their scores or anything like that.
 - Stateful - they need the application state to be maintained on some storage volume e.g in a database we are storing the users, scores, history of the games etc.
### Approaches for Stateful containers
 - -v : parameter option:
      - -v host-dir:container-dir option instructs the docker to map a host directory to a container directory. It can be a good option for some scenarios but not an effective solution. What if the container is run from another docker where the host directory does not exist?
 - Using Data Containers:
   - they are responsible for storing data
   - but they don't run like other containers
   - they hold the data/volume and are referenced by other containers who want to use this volume
### Data containers in action
 - Lets use Busybox(one of the smaller Linux distributions) we will use this container to hold our data and to be referenced by other containers
 - We will use docker create command to create a new container and pass -v parameter to create a container folder
 - We will then copy the configuration file from host folder to container folder
 - Now with the new data container created, we will use this container to reference/mount on a Ubuntu container using command --volumes-from
 - We will see how in the Ubuntu container since out container is mounted as volume, we can see the config file there.
 - This data container can be exported and imported too.
## The code is below with explanations
```
[root@mnaeemsiddiqui6 mybusybox]# # create a config file
[root@mnaeemsiddiqui6 mybusybox]# echo "test=true" >> config.conf
[root@mnaeemsiddiqui6 mybusybox]# 
[root@mnaeemsiddiqui6 mybusybox]# # create a container by a specific name , with v option to create a folder in the container
[root@mnaeemsiddiqui6 mybusybox]# # (busybox is very small container)
[root@mnaeemsiddiqui6 mybusybox]# docker create -v /config --name naeemsDataContainer busybox
Unable to find image 'busybox:latest' locally
latest: Pulling from library/busybox
f70adabe43c0: Pull complete 
Digest: sha256:58ac43b2cc92c687a32c8be6278e50a063579655fe3090125dcb2af0ff9e1a64
Status: Downloaded newer image for busybox:latest
8fb9509958311dfbc83f9dd763f9096a4a95c8d35265db9a9cc560975c13744f
[root@mnaeemsiddiqui6 mybusybox]# 
[root@mnaeemsiddiqui6 mybusybox]# 
[root@mnaeemsiddiqui6 mybusybox]# # copy data from local to the container
[root@mnaeemsiddiqui6 mybusybox]# docker cp config.conf naeemsDataContainer:/config/
[root@mnaeemsiddiqui6 mybusybox]# 
[root@mnaeemsiddiqui6 mybusybox]# # run an ubuntu container, referencing the container naeemsDataContainer using command --volumes-from
[root@mnaeemsiddiqui6 mybusybox]# docker run --volumes-from naeemsDataContainer ubuntu ls /config
Unable to find image 'ubuntu:latest' locally
latest: Pulling from library/ubuntu
a48c500ed24e: Pull complete 
1e1de00ff7e1: Pull complete 
0330ca45a200: Pull complete 
471db38bcfbf: Pull complete 
0b4aba487617: Pull complete 
Digest: sha256:c8c275751219dadad8fa56b3ac41ca6cb22219ff117ca98fe82b42f24e1ba64e
Status: Downloaded newer image for ubuntu:latest
config.conf
[root@mnaeemsiddiqui6 mybusybox]# # export the container
[root@mnaeemsiddiqui6 mybusybox]# docker export naeemsDataContainer > naeemsDataContainer.tar
[root@mnaeemsiddiqui6 mybusybox]# 
[root@mnaeemsiddiqui6 mybusybox]# # import the container
[root@mnaeemsiddiqui6 mybusybox]# docker import naeemsDataContainer.tar
sha256:4bb1c737b1b1ee89357154b45ab599bb016f4b91b42d5aa54a6bea7dcdd0637a
[root@mnaeemsiddiqui6 mybusybox]# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
<none>              <none>              4bb1c737b1b1        13 seconds ago      1.15MB
ubuntu              latest              452a96d81c30        7 days ago          79.6MB
busybox             latest              8ac48589692a        4 weeks ago         1.15MB
[root@mnaeemsiddiqui6 mybusybox]# docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED              STATUS                          PORTS               NAMES
7026a753f573        ubuntu              "ls /config"        About a minute ago   Exited (0) About a minute ago                       elated_chebys
hev
8fb950995831        busybox             "sh"                About a minute ago   Created                                             naeemsDataCon
tainer
[root@mnaeemsiddiqui6 mybusybox]# 
```
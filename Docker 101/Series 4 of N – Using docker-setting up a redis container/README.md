### Requirement:
- Lets imagine that as a DevOps, you have been asked to create a container to run redis, and try different docker commands to run redis in foreground, background, with specific port binding, with dynamic port binding, persisting data and logs from container to a volume on host

### Strategy:
- search the name of image on docker hub
- run the redis container in background as its a database and will take time to setup
- run redis in background
- run redis with specific port
- run redis with dynamic port

### Solution:
- Login to your Host machine(in my case a CentOS 7 machine)
- Make a directory “myredis ” and go to the directory – 
  ```
  mkdir myredis  && cd myredis
  ```
- To search for an image – **docker search image-name**
  ```
  docker search redis
  ``` 
- To run for an image (interractive mode) – **docker run -it image-name**
  ```
  docker run -it redis
  ```
- To run for an image (background mode) – **docker run -d image-name**
  ```
  docker run -d redis
  ```
- To check if redis container is running – **docker ps -a**
  ```
  docker ps -a
  ``` 
- To check logs on a container – docker logs container-id
  ```
  docker logs container-id # show full log
  docker logs –tail 10 container-id # show last 10 lines
  docker logs -f container-id # show continuous logs as it generates
  ```
- To stop a container – docker container stop container-id
  ```
  docker container stop a15268c9c0be
  ```
- To start a container – docker container start container-id
  ```
  docker container start a15268c9c0be
  ```
- To kill a container – docker container kill container-id
  ```
  docker container kill a15268c9c0be
  ```
- To execute redis with a specific port with host container port forwarding( not a good practice because we are hard setting the port)
   ```
   docker run -d –name redisHostStaticPort -p 6379:6379 redis:latest
   ```
 - To execute redis with a dynamic host port with host container port forwarding
   ```
   docker run -d –name redisHostDynamicPort001 -p 6380 redis:latest
   ```
 - To know which host port was assigned
   ```
   docker port redisHostDynamicPort001 6380
   ```
 - To run another instance too
   ```
   docker run -d –name redisHostDynamicPort002 -p 6381 redis:latest
   docker port redisHostDynamicPort002 6381
   ```
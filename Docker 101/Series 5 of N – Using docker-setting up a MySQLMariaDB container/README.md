### Requirement
 * Lets imagine that as a DevOps, you have been asked to create a container to run MySQL/MariaDB, and try different docker commands to run MySQL/MariaDB in foreground, background, with specific port binding, with dynamic port binding, persisting data and logs from container to a volume on host
 
### Strategy:
 * search the name of image on docker hub
 * run the MySQL/MariaDB container in background as its a database and will take time to setup
 * run MySQL/MariaDB in background
 * run MySQL/MariaDB with specific port
 * run MySQL/MariaDB with dynamic port
 * run MySQL/MariaDB with volume persistance
 
### Solution:
 * Login to your Host machine(in my case a CentOS 7 machine)
 * Make a directory “mymariadb” and go to the directory:
   ```
   mkdir mymariadb && cd mymariadb
   ```
 * Search for an image using filters and limits(e.g. filter "filter-condition" and –limit number): 
   ```
   docker search –-filter “is-official=true” –-limit 5 mariadb
   ```
 * Run an image:
   * In interactive mode and check logs- 
     ```
     docker run -it --name mymariadb-fg -e MYSQL_ROOT_PASSWORD=mypasswordfg mariadb:latest
     docker logs <containername>
     ```
   * In background mode - 
     ```
     docker run -d --name mymariadb-bg -e MYSQL_ROOT_PASSWORD=mypasswordbg mariadb:latest
     docker logs <containername>
     ```
* Now create an image and container using "docker-compose":
   * Create a file docker-compose.yml and add the following content and save:
     ```
     version: '3.1'

     services:
      db:
        image: mariadb
        restart: always
        environment:
         MYSQL_ROOT_PASSWORD: mypassword

     adminer:
      image: adminer
      restart: always
      port:
       - 8080:8080
     ```
   * Now run - docker-compose-up  ( in intercative mode) or else  docker-compose-up -d ( in background mode)
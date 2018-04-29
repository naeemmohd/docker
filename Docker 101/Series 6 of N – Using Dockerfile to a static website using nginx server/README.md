### Requirement
 * To run a static website using nginx server
 
### Strategy:
 * Docker uses a Dockerfile to define what all will be going in a container
 * For above requirement we need the following:
    * nginx web server
    * a working directory with some static html content
    * copying the contents to nginx server
    * build the app
    * push the container to Docker Hub( you will need to create Docker Hub account and a repository under the account, Please visit hub.docker.com)
    * pull the image 
    * run the container
 
### Solution:
 * Login to your Host machine(in my case a CentOS 7 machine)
 * Make a directory “myweb” and go to the directory – 
   ```
   mkdir myweb && cd myweb
   ```
 * Create a html file with some content
   ```
   echo "<h1>HI , This is a statis web page</h1>" > index.html
   ```
 * Now create a Dockerfile and copy the following content into it – 
   ```
   nano Dockerfile
   ```
 * Copy following content into the Dockerfile and save: – 
   ```
   FROM nginx:alpine
   COPY ./index.html /usr/share/nginx/html
   EXPOSE 80
   CMD ["nginx", "-g", "daemon off;"]
   ```
 * Now build the app-
   ```
   docker build -t mynginx:vNaeem .
   ```
 * Now run run the container to run the website
   ```
   docker run -d -p 80:80 mynginx:vNaeem
   ```
 * Check if the nginx server is running properly - the output should show the contents of index.html file above - <h1>HI , This is a statis web page</h1>
   ```
   curl localhost
   ```
 * Now tag the image and push to GitHub
   ```
   docker tag $(docker images mynginx:vNaeem -q) mnaeemsiddiqui/naeemsrepo:NaeemNginX
   docker push  mnaeemsiddiqui/naeemsrepo:NaeemNgin
   ```
 * Pull your tagged Docker Image and run it
   ```
   docker pull mnaeemsiddiqui/naeemsrepo:NaeemNginX
   docker run -d -p 80:80 mnaeemsiddiqui/naeemsrepo:NaeemNginX
   curl localhost
   ```
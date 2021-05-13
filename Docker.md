## Docker Basic Commands

_shows info about docker in the machine_  
`docker info` 

_run container in interactive mode (it) at port 8080 and map at 80_  
`docker container run -it -p 8080:80 nginx`  
`docker container run -d -p 8080:80 --name mynginx nginx` _detached (-d) mode_

_show containers in the system_  
`docker ps` _only active_  
`docker ps -a` _all_  

_remove container starting with id 8e10_  
`docker container rm 8e10`   
`docker container rm 8e10 -f` _if it's running, it needs to be forced_

_show all downloaded images in the system_  
`docker images`  

_get an image from https://hub.docker.com/_  
`docker pull mongo:latest`

_remove image starting with id 298_  
`docker image rm 298` 

_enviroment variables example_  
`docker container run -d -p 3306:3306 --name mysql --env MYSQL_ROOT_PASSWORD=123456 mysql`

_update docker containers_  
`docker update --restart=always 0576df221c0b`

_connect to the container_  
`docker container exec -it mynginx bash`  
`exit`

_bind localpath to the container_  
`docker container run -d -p 8080:80 -v C:\Users\themi\Docker\nginx-website:/usr/share/nginx/html --name nginx-website nginx`

## Dockerfiles

__Dockerfile example for a Node.js app__

`FROM node`

`WORKDIR /var/www/app`

`COPY . .`

`RUN npm install`

`EXPOSE 80`

`CMD ["node", "server.js"]`

_notes:_  
__WORKDIR__ is where all commants will executed (in the docker)  
__COPY__ everything from the existing folder (first dot) into the workspace (second dot)  
__RUN__ will run when an image is created  
__EXPOSE__ (optional) you still need to then actually expose the port with -p when running docker run  
__CMD__ will run when a container is starting  

_build & run_  
`docker build .`  
`docker run -p 8080:80 <ID>` _-p (publish) localPort:dockerPort_

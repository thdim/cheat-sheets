## Docker Basic Commands

`docker info` _shows info about docker in the machine_   
`docker ps --help` _get all the available options in any command_  

__run containers__  
`docker run -p 8080:80 nginx` _default is attached_   
`docker run -it -p 8080:80 nginx` _interactive terminal (-it) mode_  
`docker run -d -p 8080:80 nginx` _detached (-d) mode_  
`docker attach <id or name>` _will attach to a detached container_  
`docker logs -f <id or name>` _will show logs (like we are attached)_  
`docker stop <id or name>`  

__show containers__  
`docker ps` _only active_  
`docker ps -a` _all_  

__remove containers__  
`docker rm <id or name>`   
`docker rm <id or name> -f` _if it's running, it needs to be forced_

__images__  
`docker pull mongo:latest` _get image from https://hub.docker.com/_  
`docker images` _show images_  
`docker rmi <id>` _remove image_  
`docker image prune` _remove all (not used) images_  
`docker image inspect <id>` _shows information about an image_  

__naming & tagging__  
`docker run -p 3000:80 -d --name myname <id>`  _name a container to 'myname'_  
`docker build -t myname:latest .` _tag (-t) an image when you build it (name:tag)_  


_enviroment variables example_  
`docker container run -d -p 3306:3306 --name mysql --env MYSQL_ROOT_PASSWORD=123456 mysql`

_update docker containers_  
`docker update --restart=always 0576df221c0b`

_connect to the container_  
`docker container exec -it mynginx bash`  
`exit`



## Dockerfiles

__Dockerfile example for a Node.js app__

`FROM node:14`

`WORKDIR /var/www/app`

`COPY package.json .`

`RUN npm install`

`COPY . .`

`EXPOSE 80`

`CMD ["node", "server.js"]`

__notes__  
`WORKDIR` _is where all commants will executed (in the docker)_  
`COPY` _everything from the existing folder (first dot) into the workspace (second dot)_  
`RUN` _will run when an image is created_  
`EXPOSE` _(optional) you still need to then actually expose the port with -p when running docker run_  
`CMD` _will run when a container is starting_  

__build & run__  
`docker build .`  
`docker run -p 8080:80 <id or name>` _-p (publish) localPort:dockerPort_

## Managing Data / Volumes

_[Volumes]_
_In the Dockerfile add..._  
`VOLUME ["/var/www/app/feedback"]` _[Anonymous volume: doesn't persist] path in the docker_

_In the console after build_
`docker run -d -p 3000:80 -rm --name feedback-app -v feedback` _[Named volume: persist close]_  

_[Bind Mounts]_  
`docker container run -d -p 8080:80 -v C:\Users\themi\Docker\nginx-website:/usr/share/nginx/html --name nginx-website nginx`

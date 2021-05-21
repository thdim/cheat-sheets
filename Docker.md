## Docker Basic Commands

`docker info` _shows info about docker in the machine_   
`docker ps --help` _get all the available options in any command_  

__run & stop__  
`docker run -p 8080:80 nginx` _default is attached_   
`docker run -it -p 8080:80 nginx` _interactive terminal (-it) mode_  
`docker run -d -p 8080:80 nginx` _detached (-d) mode_  
`docker stop <id or name>`  

__attach & logs__  
`docker attach <id or name>` _will attach to a detached container_  
`docker logs -f <id or name>` _will show logs (like we are attached)_  

__show__  
`docker ps` _only active_  
`docker ps -a` _all_  

__remove__  
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

__update__  
`docker update --restart=always 0576df221c0b` _always restart_  

__connect__  
`docker container exec -it mynginx bash` _connect in the console of the container_  
`exit`  

## Dockerfiles

__Dockerfile example for a Node.js app__

`FROM node:14`

`WORKDIR /var/www/app`

`COPY package.json .`

`RUN npm install`

`COPY . .`

`ENV PORT 80`

`EXPOSE 80` or `EXPOSE $PORT`

`CMD ["node", "server.js"]`

__notes__  
`WORKDIR` _is where all commants will executed (in the docker)_  
`RUN` _will run when an image is created_  
`COPY` _everything from the existing folder (first dot) into the workspace (second dot), not needed with bind mount (developent)_  
`ENV ENV_NAME ENV_VALUE` _set an enviroment variable with ENV_NAME and ENV_VALUE_  
`EXPOSE` _(optional) you still need to then actually expose the port with -p when running docker run_  
`CMD` _will run when a container is starting_  

__.dockeringore__  
_will not COPY the listed files or folders_  
`node_modules`  
`Dockerfile`  
`.git`  

__build & run__  
`docker build .`  
`docker run -p 8080:80 <id or name>` _-p (publish) localPort:dockerPort_

## Managing Data / Volumes

__[Volumes] Controlled by Docker__  
_Anonymous volume: doesn't persist (Survives container shutdown / restart unless --rm is used)_  
_They can be used for performance_   
`docker run -v /app/data`

_Named volume: persist close (Can be shared across containers)_  
`docker run -v data:/app/data` 

__[Bind Mounts] Contolled by the user__  
`docker run -v /path/to/code:/app/code`  
`docker run -d -p 8080:80 -v C:\Users\themi\Docker\nginx-website:/usr/share/nginx/html nginx` _full example_    
`-v "%cd%":/app` _Windows shorthand for current directory (where the project is located)_  

__Managing volumes__  
`docker volume --help` _available commands about volumes_  
`docker volume ls` _lists all active volumes_  

__Enviroment variables example__  
`docker run --env MYSQL_ROOT_PASSWORD=123456 mysql`  
`docker run -e PORT=5000 -e MYSQL_PASSWORD=123456 mysql` _multiple variables with -e (shorthand for --env)_  
`docker run --env-file ./.env` _use .env file in the current directory (./) for the list of enviroment variables_

## Networking: (Cross-)Container Communication

`host.docker.internal` _use it wherever you use localhost in code in order to communicate with the hosting machine (example would be a database)_  

`docker container inspect mongodb` _inspect container with name mongodb, find the ip to use in another container (basic solution for cross container communication)_  

__Docker Network (cross-container communication)__  
`docker network create favorites-net` _create a network with name favorites-net_  
`docker run -d --name mongodb --network favorites-net mongo` _use the network_  
_replace localhost or host.docker.internal with the name of the container in the network to communicate_  

__Complete Example of a (Manual) Multi-Container App with Network__  
`docker network create goals-net`  

`docker run --name mongodb -v data:/data/db --rm -d --network goals-net -e MONGO_INITDB_ROOT_USERNAME=themis -e MONGO_INITDB_ROOT_PASSWORD=123456 mongo`  
_no ports because it will communicate in the network, volume to a local folder to save data_  

`docker run --name goals-backend -v /my/own/codedir:/app -v /my/own/datadir:/app/logs --rm -d -p 80:80 --network goals-net goals-node`  
_use the name of the database (mongodb) as domain (eg localhost) in the app, expose ports to talk with the frontend_  

`docker run --name goals-frontend -v /my/own/codedir/src:/app/src --rm -it -p 3000:3000 goals-react`  
_use localhost as a domain in the app, publich ports because you want to interact_  

## Docker Compose: (Automatic) Multi-Container Orchestration  

__docker-compose.yaml__  
`# COMMENT`  

`version: "3.8"`  

`services: `  
&nbsp;&nbsp;`mongodb:`  
&nbsp;&nbsp;&nbsp;&nbsp;`image: mongo`  
&nbsp;&nbsp;&nbsp;&nbsp;`volumes:`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`- data:/data/db`  
&nbsp;&nbsp;&nbsp;&nbsp;`enviroment:`    
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`MONGO_INITDB_ROOT_USERNAME: themis` or `- MONGO_INITDB_ROOT_USERNAME=themis`  
&nbsp;&nbsp;&nbsp;&nbsp;`env_file:`  
&nbsp;&nbsp;&nbsp;&nbsp;_# OR_  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`- ./env/mongo.env`    
&nbsp;&nbsp;`backend:`  
&nbsp;&nbsp;&nbsp;&nbsp;`build: ./backend`  
&nbsp;&nbsp;&nbsp;&nbsp;_# OR_    
&nbsp;&nbsp;&nbsp;&nbsp;`build:`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`context: ./backend`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`dockerfile: Dockerfile`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`args: `  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`some-arg: 1`  
&nbsp;&nbsp;&nbsp;&nbsp;`ports:`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`- '80:80'` 
&nbsp;&nbsp;&nbsp;&nbsp;`volumes:`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`- logs:/app/logs`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`- ./backend:/app`
&nbsp;&nbsp;`frontend:`  

`volumes:`  
&nbsp;&nbsp;`data:` _this needs to be specified if we use named volumes (it's weird but this is the syntax)_  
&nbsp;&nbsp;`logs:`


__notes__  
`version` _the docker compose version https://docs.docker.com/compose/compose-file/compose-versioning/_  
`services` _or else "containers", childs need to be 2 spaces inside_  
`volumes` _in we use a bind volume we can use relative path (./) in Docker compose_  
`config` _--rm and -d as added by default when using Docker compose_
`network` _you can do it but by default Docker compose will create a network in Docker Compose_  
`build` _the relative path to find the Dockerfile and build the container_  

__run & stop__  
`docker-compose up`  
`docker-compose up -d` _detached mode_  
`docker-compose down` _deletes containers and networks but does not delete volumes_  
`docker-compose down -v` _deletes everything, including volumes_  



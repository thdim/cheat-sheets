## Target Setup

App Containers: PHP Interpreter, Nginx Web Server, MySQL Database  
Utility Containers: Composer, Laravel Artisan, npm

## docker-compose.yaml

`version: "3.8"`  
`services:` 
`  server:`
`    image: 'nginx:stable-alpine'`  

`  php:`
`  mysql:`
`  composer:`
`  artisan:`
`  npm:`

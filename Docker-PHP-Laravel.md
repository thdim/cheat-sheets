## Target Setup

App Containers: PHP Interpreter, Nginx Web Server, MySQL Database  
Utility Containers: Composer, Laravel Artisan, npm

__docker/composer.dockerfile__  
`FROM composer:latest`  

`RUN addgroup -g 1000 laravel && adduser -G laravel -g laravel -s /bin/sh -D laravel`  

`USER laravel`  

`WORKDIR /var/www/html`  

`ENTRYPOINT [ "composer", "--ignore-platform-reqs" ]`

__docker/php.dockerfile__  
`FROM php:7.4-fpm-alpine`  

`WORKDIR /var/www/html`  

`COPY src .`  

`RUN docker-php-ext-install pdo pdo_mysql`  

`RUN addgroup -g 1000 laravel && adduser -G laravel -g laravel -s /bin/sh -D laravel`  

`USER laravel`  

__docker-compose.yaml__  
`version: "3.8"`  

`services: `  
&nbsp;&nbsp;`server:`  
&nbsp;&nbsp;&nbsp;&nbsp;`image: 'nginx:stable-alpine'`  
&nbsp;&nbsp;&nbsp;&nbsp;`ports:`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`- '8000:80'`  
&nbsp;&nbsp;&nbsp;&nbsp;`volumes:`   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`- ./src:/var/www/html`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`- ./nginx/nginx.conf:/etc/nginx/conf.d/default.conf:ro`  
&nbsp;&nbsp;&nbsp;&nbsp;`depends_on:`   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`- php`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`- mysql`  
&nbsp;&nbsp;`php:`  
&nbsp;&nbsp;&nbsp;&nbsp;`build:`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`context: .`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`dockerfile: docker/php.dockerfile`  
&nbsp;&nbsp;&nbsp;&nbsp;`volumes:`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`- ./src:/var/www/html:delegated`  
&nbsp;&nbsp;`mysql:`  
&nbsp;&nbsp;&nbsp;&nbsp;`image: 'mysql:5.7'`  
&nbsp;&nbsp;&nbsp;&nbsp;`env_file:`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`- ./env/mysql.env`  
&nbsp;&nbsp;`composer:`  
&nbsp;&nbsp;&nbsp;&nbsp;`build:`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`context: .`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`dockerfile: docker/composer.dockerfile`  
&nbsp;&nbsp;&nbsp;&nbsp;`volumes:`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`- ./src:/var/www/html`  

&nbsp;&nbsp;`artisan:`  
&nbsp;&nbsp;`npm:`  
      
__console commands__  
`docker-compose run --rm composer create-project --prefer-dist laravel/laravel .`  
`docker-compose up -d --build server`  
`docker-compose run --rm artisan migrate`  
`docker-compose run --rm artisan route:list`  


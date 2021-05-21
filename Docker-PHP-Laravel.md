## Target Setup

App Containers: PHP Interpreter, Nginx Web Server, MySQL Database  
Utility Containers: Composer, Laravel Artisan, npm

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
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`context: ./docker`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`dockerfile: php.dockerfile`  
&nbsp;&nbsp;&nbsp;&nbsp;`volumes:`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`- ./src:/var/www/html:delegated`  
&nbsp;&nbsp;`mysql:`  
&nbsp;&nbsp;&nbsp;&nbsp;`image: 'mysql:5.7'`  
&nbsp;&nbsp;&nbsp;&nbsp;`env_file:`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`- ./env/mysql.env`  
&nbsp;&nbsp;`composer:`  
&nbsp;&nbsp;&nbsp;&nbsp;`build:`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`context: ./docker`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`dockerfile: composer.dockerfile`  
&nbsp;&nbsp;&nbsp;&nbsp;`volumes:`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`- ./src:/var/www/html`  

&nbsp;&nbsp;`artisan:`  
&nbsp;&nbsp;`npm:`  
      
__console commands__  
`docker-compose run --rm composer create-project --prefer-dist laravel/laravel .`  
`docker-compose up -d server`


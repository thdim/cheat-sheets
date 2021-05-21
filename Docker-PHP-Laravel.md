## Target Setup

App Containers: PHP Interpreter, Nginx Web Server, MySQL Database  
Utility Containers: Composer, Laravel Artisan, npm

__docker-compose.yaml__  
`version: "3.8"`  

`services: `  
&nbsp;&nbsp;`server:`  
&nbsp;&nbsp;&nbsp;&nbsp;`image: 'nginx:stable-alpine'`  

&nbsp;&nbsp;`php:`  
&nbsp;&nbsp;`mysql:`  
&nbsp;&nbsp;`composer:`  
&nbsp;&nbsp;`artisan:`  
&nbsp;&nbsp;`npm:`  

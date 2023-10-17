 apt update
    2  apt --upgradable
    3  apt list --upgradable
    4  apt-get install apt-transport-https ca-certificates curl tree software-properties-common -y
    5  curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
    6  add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
    7  apt-get install docker-ce docker-compose -y
    8  cd
    9  mksdir docker-project
   10  mkdir docker-project
   11  cd docker-project/
   12  vim docker-compose.yml
------------------------------------------------
File :  nginx:   
      image: nginx:latest  
      container_name: nginx-container  
      ports:   
       - 80:80 
-----------------------------------------------
   13  docker-compose up -d
   14  docker ps
   15  mkdir /www
   16  cd /www/
   17  mkdir /html
   18  cd html
   19  cd /html
   20  vim index.php
   21  cd ..
   22  ls
   23  cd /
   24  ls
   25  ll
   26  cd rm -rf html/
   27  rm -rf html/
   28  ll
   29  cd www/
   30  ls
   31  rm www
   32  cd ..www
   33  cd 
   34  rm  www
   35  rm  -rf www
   36  ls
   37  ll
   38  cd docker-project/
   39  ls
   40  mkdir nginx
   41  mkdir nginx php
   42  mkdir php
   43  ll
   44  mkdir www
   45  ls
   46  cd www/
   47  mkdir html
   48  cd html/
   49  vim index.php
   50  cd ..
   51  ls
   52  cd nginx/
   53  vim default.conf
---------------------------------------------------------------------------
server {  

     listen 80 default_server;  
     root /var/www/html;  
     index index.html index.php;  

     charset utf-8;  

     location / {  
      try_files $uri $uri/ /index.php?$query_string;  
     }  

     location = /favicon.ico { access_log off; log_not_found off; }  
     location = /robots.txt { access_log off; log_not_found off; }  

     access_log off;  
     error_log /var/log/nginx/error.log error;  

     sendfile off;  

     client_max_body_size 100m;  

     location ~ .php$ {  
      fastcgi_split_path_info ^(.+.php)(/.+)$;  
      fastcgi_pass php:9000;  
      fastcgi_index index.php;  
      include fastcgi_params;  
      fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;  
      fastcgi_intercept_errors off;  
      fastcgi_buffer_size 16k;  
      fastcgi_buffers 4 16k;  
    }  

     location ~ /.ht {  
      deny all;  
     }  
    } 
-------------------------------------------------------------------------------------
   54  vim Dockerfile
   55  cd ..
   56  ls
   57  vim docker-compose.yml 
   58  docker-compose up -d
   59  vim docker-compose.yml 
   60  docker-compose up -d
   61  vim docker-compose.yml 
   62  docker-compose up -d
   63  vim docker-compose.yml 
   64  docker-compose up -d
   65  vim docker-compose.yml 
   66  docker-compose up -d
   67  docker ps



Dockerfile :
version: '3'
services:
  nginx:
    build: ./nginx/
    container_name: nginx-container
    ports:
      - 80:80
    links:
      - php
    volumes:
      - ./www/html/:/var/www/html/

  php:
    image: php:7.0-fpm
    container_name: php-container
    expose:
      - 9000
    volumes:
      - ./www/html/:/var/www/html/

Only nginx Docker file :



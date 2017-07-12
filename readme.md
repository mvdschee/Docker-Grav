# GRAV

### In Short
This image is optimized for use with **GRAV CMS**
+ **Nginx** as a fast and efficient webserver.
+ **PHP-FPM** as the FastCGI engine.
+ **Pushion** as the minimal Linux container for this image.
+ **Let's Encrypt** as the certificate authority.

### Usage
**Only works with Docker-Compose**

**Example non-ssl:**

*docker-compose.yml*

    version: '2'

    services:
       grav:
         image: maxvanderschee/grav:latest
         volumes:
           - /var/www/YOURWEBSITE:/var/www/app
         environment:
           CONF: non-ssl.conf
           APPURL: YOURWEBSITE.COM
           SUBAPPURL: WWW.YOURWEBSITE.COM
         ports:
           - "80:80"

The last step is to excute the bashscript:
``docker exec CONTAINER_NAME bash /root/bash.sh``

**Example ssl:**

*docker-compose.yml*

    version: '2'

    services:
      grav:
        image: maxvanderschee/grav:latest
        volumes:
          - /var/www/YOURWEBSITE:/var/www/app
          - /root/archive:/etc/letsencrypt/archive
        environment:
          CONF: ssl.conf
          APPURL: YOURWEBSITE.COM
          SUBAPPURL: WWW.YOURWEBSITE.COM
        ports:
          - "80:80"
          - "443:443"

The next step is to login to the container and execute:

``sudo letsencrypt certonly -a webroot --webroot-path=/var/www/app -d YOURWEBSITE.COM -d www.YOURWEBSITE.COM``

`` bash /root/bash.sh``

### Dockerfile

+ Define the base image as **maxvanderschee/nginx-php**.
+ Install and update the core components for this new container like PHP7.0-cli, PHP7.0-gd, etc.

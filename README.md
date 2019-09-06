# php_xdebuger_docker
Some simple dockerfiles are design for php debugging jobs.It is easy to build a runtime environment for simple php application.

## Notice
From 18.03 onwards docker recommendation is to connect to the special DNS name host.docker.internal, which resolves to the internal IP address used by the host. This is for development purpose and will not work in a production environment outside of Docker Desktop for Mac.

## Examples
```
➜  phpipxx cat docker-compose.yml 
version: '3.3'

services:
  mysql:
    image: mysql:5.6
    environment:
      - MYSQL_ROOT_PASSWORD=toor
  ipam:
    depends_on:
      - mysql
    image: phpx.x_xdebug_dockerxxx
    ports:
      - "127.0.0.1:80:80"
    volumes:
      - ./ipxxsource:/var/www/html
```

```
➜  wordpress4.7.6 cat docker-compose.yml 
version: '3.3'

services:
  db:
    image: mysql:5.7
    restart: on-failure
    environment:
      MYSQL_ROOT_PASSWORD: somewordpress
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: wordpress

  wp:
    depends_on:
      - db
    image: 2ndGeorge/wordpress-xdebug:4.7.3
    volumes:
      - ./wp:/var/www/html
    ports:
      - 127.0.0.1:81:80
    restart: on-failure
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_USER: wordpress
      WORDPRESS_DB_PASSWORD: wordpress
      XDEBUG_CONFIG: "remote_host=host.docker.internal remote_port=9001"
```
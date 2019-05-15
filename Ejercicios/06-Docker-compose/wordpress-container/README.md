# wordpress container with **docker-compose**

#### Useful links
[Docker compose - Wordpress](https://docs.docker.com/compose/wordpress/)

## Step 1
Create folder in **/var/containers**

## Step 2
Create file **docker-compose.yml** with this code:

```
version: '3.3'

services:
  db:
    image: mysql:5.7
    volumes:
      - db_data:/var/lib/mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: somewordpress
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: wordpress

  wordpress:
    depends_on:
      - db
    image: wordpress:latest
    ports:
      - "8000:80"
    restart: always
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_USER: wordpress
      WORDPRESS_DB_PASSWORD: wordpress
      WORDPRESS_DB_NAME: wordpress
volumes:
  db_data: {}

```

## Step 3

Change to /var/container/**{my_folder}** and execute this command:
```
docker-compose up -d
```

## Step 4
Check [localhost:8000](http://localhost:8000)


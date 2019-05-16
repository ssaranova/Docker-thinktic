# Introducción Docker-compose auto arranque

Y en **/etc/systemd/system/** añadimos el fichero **docker-compose@.service**
con el siguiente contenido:

```
[Unit]
Description=%i service with docker compose
Requires=docker.service
After=docker.service

[Service]
Restart=always
 
WorkingDirectory=/etc/docker/compose/%i
 
# Remove old containers, images and volumes
ExecStartPre=/usr/bin/docker-compose down -v
ExecStartPre=/usr/bin/docker-compose rm -fv
ExecStartPre=-/bin/bash -c 'docker volume ls -qf "name=%i_" | xargs docker volume rm'
ExecStartPre=-/bin/bash -c 'docker network ls -qf "name=%i_" | xargs docker network rm'
ExecStartPre=-/bin/bash -c 'docker ps -aqf "name=%i_*" | xargs docker rm'
 
# Compose up
ExecStart=/usr/bin/docker-compose up
 
# Compose down, remove containers and volumes
ExecStop=/usr/bin/docker-compose down -v
 
[Install]
WantedBy=multi-user.target
```


Y necesitamos que system ctl recarge los ficheros mediante el comando
```
$ systemctl daemon-reload 
$ systemctl enable docker-composer.service
$ systemctl start docker-composer.service
$ systemctl status docker-composer.service
```
a partir de aqui

En  **/etc/docker/compose** meter o crear los enlaces a los distintos docker-compose con su directorio o un "ln -s /xxxxxx"
Por ejemplo:
```
ln -s /var/containers/wordpress /etc/docker/compose/
```

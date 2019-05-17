Set domain name in **--docker.domain**

Set IP in **traefik.frontend.rule=Host:**
- *127.0.0.1* for self purpose
- *ifconfig IP* for net purposes
- subdomain.domain for online purposes

Set your images/services **label** like your **subdomain**


edit /etc/hosts
``127.0.0.1 portainer.mywebdomain.com``
``127.0.0.1 ms1.mywebdomain.com``


RUN: 

{stack_name} -> traefik

``
$ docker stack deploy -c traefik-compose.yml {stack_name}
$ docker service ls
$ docker image ls
``


URLS

portainer: ``portainer.mywebdomain.com``
m1: ``ms1.mywebdomain.com``
traefik: ``127.0.0.1:8080`
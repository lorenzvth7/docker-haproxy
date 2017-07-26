# docker-haproxy
Easy HAproxy example:


```
$ docker-compose up -d --build
```

```
$ docker ps
CONTAINER ID        IMAGE                        COMMAND                  CREATED             STATUS              PORTS                NAMES
9c4d73849495        dockerhaproxy_haproxy        "/docker-entrypoin..."   2 seconds ago       Up 2 seconds        0.0.0.0:80->80/tcp   haproxy
d339129f080e        dockerhaproxy_apache-php-2   "docker-php-entryp..."   2 seconds ago       Up 2 seconds        80/tcp               apache-php-2
b4630777daf4        dockerhaproxy_apache-php-1   "docker-php-entryp..."   2 seconds ago       Up 2 seconds        80/tcp               apache-php-1
```
```
$ docker network ls
NETWORK ID          NAME                    DRIVER              SCOPE
f3725c4c27f4        dockerhaproxy_default   bridge              local
```

Check in browser or with curl the haproxy:
Local machine:  
```
docker run --rm --network=dockerhaproxy_default tutum/curl /bin/bash -c 'for i in $(seq 1 10); do curl -s haproxy && echo " "  ; done'
```

Remote machine: 
```
docker run --rm tutum/curl /bin/bash -c 'for i in $(seq 1 10); do curl -s http://host-ip:80 && echo " "  ; done'
```

Expected output:
```
My container IP is 172.18.0.2
My container IP is 172.18.0.3
My container IP is 172.18.0.2
My container IP is 172.18.0.3
My container IP is 172.18.0.2
My container IP is 172.18.0.3
...
```


http://docs.docker.io/en/latest/

## TOP
Ver ps de la maquina
docker top <instance-id>

## PS
Comandos corriendo en las máquinas.
docker ps

Histórico de los comandos ejecutados en las VM
docker ps -a

## LOGS
Mensajes stderr y stdout de la máquina
docker logs <instance-id>

## STOP
docker stop <container-id>

## RESTART
docker restart <container-id>

## CP
Copia ficheros a/desde un container
docker cp IMAGE URL PATH

## RMI
Borra una imagen y todas sus dependencias (hacia abajo) no usadas.
Borra todas las imágenes con ese nombre.
Podemos hacer: rmi imagen:latest   o   rmi imagen:tag

## RM
Borra un container


## INSPECT
Información sobre un container o imagen
docker inspect <image/container-id>
docker image nombre:tag
Es como leer el fichero 
/var/lib/docker/graph/<id>/json para images
/var/lib/docker/containers/<id>/config.json para containers

## Conectar a docker no localhost
docker -H servidor:2375 ....

Correr un servicio y mapear un puerto:
docker run -p 80 user/image /usr/bin/httpd
  -p mapea el puerto 80 a uno local. Podemos ver cual con docker ps

Se elegir el puerto del host donde queremos mapear con -p 80:8080
Esto no se debe hacer en los Dockerfile, pues no podríamos arrancar dos container iguales.


El puerto elegido es aleatorio (creo).
Para verlo podemos hacer:
docker port <image-id> <puerto-VM>
docker inspect | less  (y buscar por Port Mapping)
docker ps  (y mirar la última columna)


# Network - UFW 
Por defecto se dropea todo el tráfico. Para cambiar la política
/etc/default/ufw
DEFAULT_FORWARD_POLICY="ACCEPT"

sudo ufw reload


Las máquinas obtienen una ip de red local 172.x.x.x
Podemos conectar con ellas directamente a través de esta ip.
Si forwardeamos un puerto lo que estamos haciendo es crear una regla en iptables para enlazar un puerto local nuestro al puerto de esa máquina.
Así podemos publicar puertos de las VM, que si no, no tienen visión desde el exterior.
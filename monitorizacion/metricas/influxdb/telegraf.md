https://github.com/influxdata/telegraf
https://docs.influxdata.com/telegraf/v0.10/introduction/getting-started-telegraf/

Telegraf is an agent written in Go for collecting metrics from the system it's running on, or from other services, and writing them into InfluxDB.

# Instalación
https://github.com/influxdata/telegraf#linux-deb-and-rpm-packages

Bajando el rpm linkado en la web e instalado a mano

Instalado la 0.10.0

yum install telegraf


# Configuración
Por defecto el rpm genera:
/etc/telegraf/telegraf.conf

Tambien  podemos pedir al binario que genere una conf de ejemplo.
Esta conf nos da mucha más opciones configuradas, mas outputs y plugins.
telegraf -sample-config

También se pueden meter configs en:
/etc/telegraf/telegraf.d

## Conf server
[[outputs.influxdb]]
  urls = ["http://10.5.2.180:8086"]
  database = "nombre" # NO poner guiones (-)
  precision = "s"

  username = "adri"
  password = "adri"


# Run
Ver que metricas se generan por stdout y salir:
telegraf -config /etc/telegraf/telegraf.conf -test

## Centos 7
systemctl start telegraf

## Centos 6
service telegraf start


# Plugins
Para ver ayuda de un cierto plugin:

telegraf -usage NOMBRE

## nagios
https://github.com/influxdata/telegraf/blob/master/docs/DATA_FORMATS_INPUT.md#nagios

## dig / dns
Nos devuelve tiempos de respuesta del servidor dns

## exec
Ejecuta un programa que debe devolver las métricas en formato inline, graphite o json


## Apache
https://github.com/influxdata/telegraf/tree/master/plugins/inputs/apache

[[inputs.apache]]
  urls = ["http://127.0.0.1/server-status?auto"]

## MongoDB
https://github.com/influxdata/telegraf/tree/master/plugins/inputs/mongodb

/etc/telegraf/telegraf.d/mongodb.conf
[[inputs.mongodb]]
  servers = ["127.0.0.1:27017"]

## httpjson
https://github.com/influxdata/telegraf/tree/master/plugins/inputs/httpjson

Hace un get a un endpoint y espera un json con valores que sean métricas.

## json - influxdb
https://github.com/influxdata/telegraf/tree/master/plugins/inputs/influxdb

Como el anterior, pero esperando un formato determinado del json

## net response / check_tcp check_udp
https://github.com/influxdata/telegraf/tree/master/plugins/inputs/net_response

Conecta a un puerto y ve cuanto tiempo tarda en contestar.

## nginx
https://github.com/influxdata/telegraf/tree/master/plugins/inputs/nginx

[[inputs.nginx]]
  ## An array of Nginx stub_status URI to gather stats.
  urls = ["http://localhost/status"]

## ping
envia ping a un server y mide tiempo de respuesta

## procstat
https://github.com/influxdata/telegraf/tree/master/plugins/inputs/procstat

Monitoriza un proceso usando los valores de /proc/PID/...
Si en el regex ponemos "." monitorizará todos los procesos

/etc/telegraf/telegraf.d/procs.conf 
[[inputs.procstat]]
  user = "icinga"
[[inputs.procstat]]
  pattern = "graphios"


## sensors
https://github.com/influxdata/telegraf/tree/master/plugins/inputs/sensors

Utiliza lm-sensors para obtener información de temperatura, ventiladores, etc

## snmp
Obtiene valores de snmp

Tendremos que cargar el mapeo de nombre de oid a número.

collect = ["interface_speed", "if_number", "if_out_octets"]
aqui ponemos nombre de cosas que vamos a definir mas tarde

Si queremos coger un único valor:
  [[inputs.snmp.get]]
    name = "if_number"
    oid = "ifNumber"

Si hay ese oid es un arbol y solo queremos coger uno:
  [[inputs.snmp.get]]
    name = "interface_speed"
    oid = "ifSpeed"
    instance = "1"

Si queremos coger todo un arbol:
  [[inputs.snmp.bulk]]
    name = "if_out_octets"
    oid = "ifOutOctets"

Este último creará una medida ifOutOctets con un único valor (ifOutOctets) y tags por cada uno de los elementos del arbol

## sysstat
https://github.com/influxdata/telegraf/tree/master/plugins/inputs/sysstat

## http reponse
https://github.com/influxdata/telegraf/tree/master/plugins/inputs/http_response

## Parse logs
https://github.com/influxdata/telegraf/blob/master/plugins/inputs/logparser/README.md

## Github
Puede levantar un puerto donde apuntamos un webhook de github


# Consumo
Con la instalación básica haciendo pooling cada 10"
  15MB 0.25%

Metiendo procstat para todos los procesos (el resto básico, con pooling cada 10"):
  17.7MB 2.29%
  aunque la memoria seguia creciendo poco a poco
  el consumo de cpu tenia bastante variación

Metiendo procstat para todos los procesos (el resto básico, con pooling cada 30"):
  16.4MB 0.7%


# Internals
Si usamos UDP envia tramas de payload 512bytes:
https://github.com/influxdata/influxdb/blob/616da49019703338da893ea6a619beebeb51f755/client/v2/client.go#L21
https://github.com/influxdata/influxdb/blob/616da49019703338da893ea6a619beebeb51f755/client/v2/client.go#L334

Si usamos HTTP:
Envia toda la info que le pasamos a la función Write:
https://github.com/influxdata/influxdb/blob/616da49019703338da893ea6a619beebeb51f755/client/v2/client.go#L354

Parece que telegraf genera un gran array de metricas y se lo pasa a write:
https://github.com/influxdata/telegraf/blob/master/plugins/outputs/influxdb/influxdb.go#L135

Por aqui está como corre el agente:
https://github.com/influxdata/telegraf/blob/master/agent/agent.go

No me queda claro como hace el write y si lo hace de todas las métricas de golpe

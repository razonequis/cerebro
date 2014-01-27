#http://www.cyberciti.biz/tips/linux-audit-files-to-see-who-made-changes-to-a-file.html

Nos sirve para guardar registro de cualquier cambio que se produzca en nuestro sistema: ficheros, syscalls, etc
Se debe ejecutar como root.

Mostrar todas las reglas:
# auditctl -l

Vigila el fichero /etc/passwd ante lecturas(r), escrituras(w), ejecuciones(x) y atributos(a)
Le asigna la palaba "password-file", para poder luego buscar estas interacciones
# auditctl -w /etc/passwd -p rwxa -k password-file

El path debe ser absoluto.

Para buscar sucesos:
Por clave
# ausearch -k clave

Por comando que lo abre/ejecuta/escribe/añade
# ausearch -c cmd

Por fichero:
# ausearch -f /path/to/file

Si queremos que traduzca los números (por ejemplo, uid por nombre)
# ausearch -i ...

Borrar todas las reglas (dara como resultado un 'No rules', es lo correcto)
# auditctl -D

O alguna en concreto:
-d <l,a>            Delete rule from <l>ist with <a>ction
                        l=task,exit,user,exclude
			a=never,always

Para borrar los resultados deberemos borrar los ficheros que están en /var/log/auditd/


En las debian no viene instalado por defecto:
apt-get install auditd
service auditd start


Parece que con LXC no funciona
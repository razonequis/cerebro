Gestión de librerías para python.
Sería como un apt-get para python.
$ pip search <libreria>
$ pip install <libreria>
$ pip install MySQL_python==1.2.2
$ pip install -t lib/ psycopg2
  instalar en el dir lib/
$ pip install --upgrade <paquete>
$ pip install --index-url http://mirror.de.pip/pypi/pypi/simple python27-cffi
$ pip install -Iv http://sourceforge.net/projects/mysql-python/files/mysql-python/1.2.2/MySQL-python-1.2.2.tar.gz/download
  -I: ignore previous versions installed
  -v: verbose
$ pip install --use-wheel <paquete>
  instala el binario si esta disponible
$ pip show --files SomePackage
$ pip uninstall <libreria>
$ pip list


## Proxy ## es https_proxy, NO http_proxy
https_proxy=http://web-proxy.mydomain.com pip install paquete
pip install --proxy="user:password@server:port" yourpackage


Mirar curdling.md para una versión más rápida


# freeze #
Obtener una lista de las versiones que estamos usando de las dependencias
pip freeze > requirements.txt

To answer the second part of this question, the two packages shown in pip list but not pip freeze are setuptools (which is easy_install) and pip itself. It looks like pip freeze just doesn't list packages that pip itself depends on. 


# Requested XXXX==N, but installing version M
Borrar /tmp/pip-build-root/XXXX

Bajar un archivo y que tenga el mismo nombre local que remoto
curl -O http://web.com/archivo.tgz

Se loguea contra el php, enviando la información como POST, guardando la cookie que nos contesten, y mostrando lo que se devuelve (-v)
curl -v -c cookies.txt -d "tfUsername=admin&tfPassword=admin&Submit=Login" http://10.6.2.5/nagiosql/index.php

Con la cookie del logueo, enviamos una petición post:
curl -v -b cookies.txt -d "butValue1=Do+it" http://10.2.2.1/nagiosql/admin/verify.php
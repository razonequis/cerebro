# http://www.cyberciti.biz/faq/appy-patch-file-using-patch-command/

diff -Naur standard_moodle my_moodle > patch.txt

patch < /path/to/file
  para hacerlo así el fichero debe decir a quien va a patchear. No tengo muy claro como se hace

Otra opción
patch fichero_a_parchear < parche


patch -N -r - fichero < parche
  para hacer la operacion idempotente
  -N permite aplicar dos veces el mismo parche
  -r -, envia la salida de -N a /dev/null

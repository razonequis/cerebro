dd if=/dev/zero of=file count=2048
  crear fichero de 1MB

Se puede pasar un parámetro para escribir con O_DIRECT (sin caches ni readahead)


Crear fichero de 1GB
fallocate -l 1G test.img
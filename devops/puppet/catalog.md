http://manpages.ubuntu.com/manpages/precise/en/man8/puppet-catalog.8.html

puppet catalog find CERTNAME

Para obtener el CERTNAME
puppet cert list --all

Buscar solo los recursos tipo file:
puppet catalog select node1.inet file
  Aqui veo recursos file que no se aplican a este nodo :?

Ver que clases se aplican a cada nodo
puppet catalog select node class

Listado de las máquinas que usan este puppet master
puppet cert list --all | awk '{print $2;}' | tr -d "\"" > lista_maquinas
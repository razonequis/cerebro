Github
Solo ofrece repositorios públicos

Gittoriuos


Bitbucket
Ofrece repositorios privados, con un límite de 5 usuarios
Cuidado al importar la clave, que no haya cambios de línea debido al copy&paste.


Mi propio servidor
Para tener un servidor que funcione como github o bitbucket
En el servidor:
	$ git init
	$ git config --bool core.bare true
	
En el cliente:
	$ git this (git init && git add . && git commit -m "initial commit")
	$ git remote add origin ssh://ncer@sun/home/repositorios/nuevo/

Convertir fecha unix timestamp a normal:
date --date @1012312312
date -d @1012312312

Fecha en timestamp con nanoseconds
date +%s.%N

Convertir fecha a unix timestamp:
date -d "Wed, 6 Oct 2010 10:43:25 +0200" +"%s"

$ LC_ALL=C date
Thu Oct  1 08:47:24 CEST 2015
$ LC_ALL=C date -d "Thu Oct  1 08:47:24 CEST 2015" +%s
1443682044

date +%F
YYYY-MM-DD

Mes del año sin cero delante:
date +%-m
6

Se puede poner más cosas:
- sin padding
_ padding con espacios
0 padding con ceros
^ uppercase
# downcase

date +%j
dia del año

Horas y minutos:
date +%H%M

Definir fecha:
date -s "Wed, 6 Oct 2010 10:43:25 +0200"
Tener cuidado con las locale (intentar pasar una fecha en español a un sistema en inglés)


$ date -Ins
2015-03-09T10:09:17,292535328+0100

Poner la hora actual más una hora:
date -d '+1 hour' "+%d.%m.%Y %H:%M:%S"
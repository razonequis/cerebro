VAR=cosa
echo $VAR

Para asignarle el resultado de un comando:
VAR=$(ifconfig)
 
ENTRE LA VARIABLE Y EL IGUAL NO PUEDE HABER ESPACIOS


Definir valor por defecto:
echo "para que nunca salga null la variable: ${variable:-valorDefault}"

${parameter:-word}
If parameter is unset or null, the expansion of word is substituted. Otherwise, the value of parameter is substituted.
${parameter:=word}
If parameter is unset or null, the expansion of word is assigned to parameter. The value of parameter is then substituted. Positional parameters and special parameters may not be assigned to in this way.
${parameter:?word}
If parameter is null or unset, the expansion of word (or a message to that effect if word is not present) is written to the standard error and the shell, if it is not interactive, exits. Otherwise, the value of parameter is substituted.
${parameter:+word}
If parameter is null or unset, nothing is substituted, otherwise the expansion of word is substituted.


Mas acciones con las variables según si están definidas o no:
http://www.debuntu.org/how-to-bash-parameter-expansion-and-default-values/


Concatenar:
foo="Hello"
foo="$foo World"
echo $foo

http://www.openssh.com/legacy.html

Unable to negotiate with 217.160.71.110: no matching host key type found. Their offer: ssh-dss
ssh -oHostKeyAlgorithms=+ssh-dss user@host

El servidor no acepta la clave pública.
Mirar si selinux está activado.

Too many authentication failures for
  -> mirar max_auth_tries.md

Mucho tiempo en logear
http://injustfiveminutes.com/2013/03/13/fixing-ssh-login-long-delay/

Utilidad para meter nuevos certificados en el sistema.

update-ca-certificates is a program that updates the directory /etc/ssl/certs to hold SSL certificates and generates certificates.crt, a concatenated single-file list of certificates.

It reads the file /etc/ca-certificates.conf. Each line gives a pathname of a CA certificate under /usr/share/ca-certificates that should be trusted. Lines that begin with "#" are comment lines and thus ignored. Lines that begin with "!" are deselected, causing the deactivation of the CA certificate in question.

Furthermore all certificates found below /usr/local/share/ca-certificates are also included as implicitly trusted


Más sencillo, usar:
sudo cp fichero.pem /usr/local/share/ca-certificates/fichero.crt
sudo dpkg-reconfigure ca-certificates
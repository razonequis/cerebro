https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Networking_Guide/sec-Using_the_NetworkManager_Command_Line_Tool_nmcli.html
man nmcli-examples

Alamcena la configuración en /etc/NetworkManager

Dos conceptos, connection and interface.

Las interfaces es solo la tarjeta de red.
Connection contiene nombre, firewall zone, ipv4 addr, ipv6 addr and interface

nmcli device wifi list
  mostrar WiFis disponibles

nmcli c s
  mostrar conexiones

nmcli d s
  mostrar devices

Servers DNS cogidos por DHCP:
  nmcli dev show | grep DNS

nmcli c e
  nos abre una "shell" inteligente para editar una conexión
  nos preguntará que tipo de conex queremos crear
  podemos poner por ejemplo 'help'

nmcli c load fichero
  recargar un fichero de conf del NM

nmcli con modify DHCP connection.autoconnect-priority 0
  cambiar la prioridad de la conex "DHCP" a 0
  cuanto mayor es el número, más prioridad (por defecto 0)


# Crear una nueva red a mano
nmcli c edit type ethernet con-name "conex-prueba"
nmcli> set ipv4.addresses 10.1.1.3
¿Desea también establecer 'ipv4.method' a 'manual'? [yes]:
nmcli> set ipv4.gateway 10.1.1.1
nmcli> set ipv4.dns
Ingresar el valor 'dns': 8.8.8.8
nmcli> set connection.autoconnect no
nmcli> save
Conexión 'conex-prueba' (0fae8ee8-01fe-469b-b40f-a9b594e48e39) guardada con éxito.


Para DHCP:
ipv4.method: auto



# Quitar un dispositivo del NM
Para desactivar un dispositivo (para que no lo maneje networkmanager):

/etc/NetworkManager/NetworkManager.conf
[keyfile]
#unmanaged-devices=mac:74:de:2b:ef:5b:71


systemctl restart NetworkManager


Propiedades:
https://developer.gnome.org/NetworkManager/stable/ref-settings.html



# Bridge
nmcli c e type bridge
nmcli> set connection.autoconnect no
nmcli> set connection.interface-name "bridge-prueba"
nmcli> set bridge.stp no
faltan algunos pasos

Luego tendriamos que crear los bridge-slaves

Los ficheros se generan en /etc/sysconfig/network-scripts/


# Debug
https://wiki.gnome.org/Projects/NetworkManager/Debugging

sudo dbus-send --system --print-reply --dest=org.freedesktop.NetworkManager /org/freedesktop/NetworkManager org.freedesktop.NetworkManager.SetLogging string:"debug" string:""

journalctl -fu NetworkManager.service


       Example 4. Listing NetworkManager log level and domains

           $ nmcli general logging
           LEVEL  DOMAINS
           INFO   PLATFORM,RFKILL,ETHER,WIFI,BT,MB,DHCP4,DHCP6,PPP,WIFI_SCAN,IP4,IP6,A
           UTOIP4,DNS,VPN,SHARING,SUPPLICANT,AGENTS,SETTINGS,SUSPEND,CORE,DEVICE,OLPC,
           WIMAX,INFINIBAND,FIREWALL,ADSL,BOND,VLAN,BRIDGE,DBUS_PROPS,TEAM,CONCHECK,DC
           B,DISPATCH

       This command shows current NetworkManager logging status.

       Example 5. Changing NetworkManager logging

           $ nmcli g log level DEBUG domains CORE,ETHER,IP
           $ nmcli g log level INFO domains DEFAULT

       The first command makes NetworkManager log in DEBUG level, and only for CORE, ETHER and IP domains. The second command restores the default
       logging state. Please refer to the NetworkManager.conf(5) manual page for available logging levels and domains.

# HotSpot
Configuración:
/etc/NetworkManager/system-connections/Hotspot
Si tocamos el fichero:
systemctl restart NetworkManager


# Dispatcher
https://wiki.archlinux.org/index.php/NetworkManager#Network_services_with_NetworkManager_dispatcher

Ejecutar scripts cuando arranca o para una interfaz.

Los scripts se ponen en /etc/NetworkManager/dispatcher.d
Deben pertenecer a root:root y modo 755.

Al llamarlos networkmanager pasa como primer parámetro la interfaz y como segundo el estado de esta:
Ejemplo:
./script eth0 up
./script wlan0 down

En los ficheros dispatcher_variables* tengo las variables disponibles al hacer down y up.

En el script, si hacemos un echo lo sacará en el journalctl como:
jun 10 08:15:57 archer nm-dispatcher[11642]: hola

journalctl -fn 100 _COMM=nm-dispatcher

Ejemplo gestion redes en: 30_trabajo.sh


# Configuracion
Explicacion de los parámetros
man nm-settings
man nm-settings-keyfiles

Ejemplos: https://cgit.freedesktop.org/NetworkManager/NetworkManager/tree/src/settings/plugins/keyfile/tests/keyfiles

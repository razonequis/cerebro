Por defecto: /etc/ansible/hosts
http://docs.ansible.com/intro_inventory.html#group-variables

Variables que podemos pasar en el inventario:
http://docs.ansible.com/intro_inventory.html#list-of-behavioral-inventory-parameters

Podemos pasarlo por linea de comandos: ansible -i fichero ...

Es case-sensitive.

Para ver nuestro inventario:
ansible all --list-hosts

Aqui definimos los grupos de máquinas.
También podemos definir variables de esas máquinas.

# Sin grupo
maquina1.com
maquina2.host.com
192.168.3.2

[webservers]
www.machine.com
webserver.host.com

[mailserver]
superserver ansible_ssh_host=smtp.host.com
pop3.host.com
mail.pepe.com
jumper ansible_ssh_port=5555 ansible_ssh_host=192.168.1.50


También podemos usar patterns:
www[001:006].example.com
db-[99:101]-node.example.com


Definiendo variables:
nombredelnodo ansible_sudo_pass='password' variable='valor'

[atlanta:vars]
ntp_server=ntp.atlanta.example.com
proxy=proxy.atlanta.example.com


If the host is named ‘foosball’, and in groups ‘raleigh’ and ‘webservers’, variables in YAML files at the following locations will be made available to the host:
/etc/ansible/group_vars/raleigh
/etc/ansible/group_vars/webservers
/etc/ansible/host_vars/foosball

Podemos tambien crear un grupo de grupos (debera llevar la coletilla children). Solo podremos meter grupos, no hosts sueltos:
[spain:children]
madrid
barcelona
valencia

[spain:vars]
ansible_sudo_pass='pepe'

Ahora podremos definir un fichero
group_vars/spain
Que afectará a todos esos grupos de máquinas


No podemos definir variables complejas (por ejemplo una lista) en el inventario. Usaremos un .yaml en groups_vars o host_vars

# Contraseñas / Passwords #
Creamos un grupo (o grupo de grupos), luego creamos su ficheros en vars:
ansible-vault create groups_vars/NOMBRE

Ahí metemos las passwords:
ansible_ssh_pass: contraseña1
ansible_sudo_pass: contraseña2

# SSH key
ansible_ssh_private_key_file=~/fichero


# Añadir máquinas al inventario desde un playbook, solo para esa ejecucción (in-memory)
http://docs.ansible.com/add_host_module.html

- add_host: hostname={{ new_ip }}
            ansible_ssh_host={{ inventory_hostname }}
            ansible_ssh_port={{ new_port }}
            groups=just_created foo=42

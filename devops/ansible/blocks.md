http://docs.ansible.com/ansible/playbooks_blocks.html

# Juntar tareas con un mismo condicional o ciertas variables generales
   tasks:
     - block:
         - yum: name={{ item }} state=installed
           with_items:
             - httpd
             - memcached

         - template: src=templates/src.j2 dest=/etc/foo.conf

         - service: name=bar state=started enabled=True

       when: ansible_distribution == 'CentOS'
       become: true
       become_user: root


# Error handling

- name: a play that runs entirely on the ansible host
  hosts: 127.0.0.1
  connection: local
  gather_facts: false
  tasks:
   - block:
       - debug: msg='i execute normally'
       - command: /bin/false
       - debug: msg='i never execute, cause ERROR!'
     rescue:
       - debug: msg='I caught an error'
       - command: /bin/false
       - debug: msg='I also never execute :-('
     always:
       - debug: msg="this always executes"


Si tenemos varios blocks, cada uno de ellos, como unidad, siempre devolverá OK.
Si queremos salir fallando de manera controlada podemos hacer:
   - block:
       - include: mio.yml
     rescue:
       - debug: msg='error en mio'
       - fail: msg="saliendo tras enviar el mensaje"


Los blocks son tasks.
No se puede hacer un playbook empezando con un block.

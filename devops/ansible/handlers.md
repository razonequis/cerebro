http://docs.ansible.com/playbooks_intro.html#handlers-running-operations-on-change

Son los que se encargan del reinicio de los servicios.
Son ejecutados solo una vez aunque sean llamados varias veces.
Se ejecutan en el orden de escritura, no el orden que sean llamados.

    - name: Restart nginx
      service: name=nginx state=restarted

    # Tambien podemos meter chequeos
    - name: Check nginx
      wait_for: port={{ nginx_port }} delay=5 timeout=10

    # Any module can be used for the handler action
    - name: Restart application
      command: /srv/myapp/restart.sh

    # Pacemaker con pcs:
    - name: Restart pnp4nagios worker
      run_once: True
      shell: /usr/sbin/pcs resource meta {{rsc}} target-role=Stopped; sleep 3; /usr/sbin/pcs resource meta {{rsc}} target-role=Started



Se llaman desde un comando con:
    - name: roll out new code
      git: repo=ssh://git@github.com/mylogin/hello.git dest=/home/mylogin/hello
      notify:
        - Restart nginx
        - Restart application

Realizar tareas de los handlers sin esperar al final
tasks:
   - shell: some tasks go here
   - meta: flush_handlers
   - shell: some other tasks

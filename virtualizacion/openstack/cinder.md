https://wiki.openstack.org/wiki/Cinder

Cinder provides an infrastructure for managing volumes in OpenStack. It was originally a Nova component called nova-volume, but has become an independent project since the Folsom release.

While Cinder contains many different storage drivers, the most common and basic configuration uses LVM and iSCSI. This guide illustrates how to use one disk (/dev/sdb) in an LVM Volume Group called cinder-volumes. When a user requests a block storage volume, a Logical Volume is created from this Volume Group and then mounted on the user's instance by way of iSCSI.
http://docs.openstack.org/grizzly/basic-install/apt/content/basic-install_controller.html


Quality Of Service.
A partir de la release Icehouse se puede dar valores a los backend donde se almacena la información para después afinar donde queremos crear nuestros volumenes.

Volume Types: para poder elegir en que Storage Tier queremos nuestro volumen (HDD, HDD-SSD, SSD, ...)
Con volume retype podemos cambiar esto una vez creado el volumen.


Mostrar imagenes almacenadas en ceph:
rados ls --pool images | grep "rbd_id"


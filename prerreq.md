

A) ASIGNACION DE ESPACIO
========================

* Log in como root
 $ su -

* Ejecutar el comando:

 $ lvextend -l +100%FREE /dev/centos/root

* Extender el FS:

 $ xfs_growfs /

1) SOFTWARE BASE
================

a) Instalar base de software

 # yum install git

 # yum group install -y "Development Tools"

 #  yum  -y install  qemu-kvm  libvirt virt-install bridge-utils  libvirt-devel \
libxslt-devel libxml2-devel libvirt-devel libguestfs-tools-c

 # echo "net.ipv4.ip_forward = 1"|sudo tee /etc/sysctl.d/99-ipforward.conf

 # sysctl -p /etc/sysctl.d/99-ipforward.conf

b) Iniciar y habilitar servicio libvirtd

 # systemctl enable libvirtd
 # systemctl start libvirtd


2) VAGRANT
==========
a) Software base:

 # wget https://releases.hashicorp.com/vagrant/1.7.4/vagrant_1.7.4_x86_64.rpm
 # yum localinstall -y vagrant_1.7.4_x86_64.rpm
 # vagrant plugin install vagrant-libvirt

b) Descargar box's vagrant

 # vagrant  box  add generic/centos7 https://vagrantcloud.com/generic/centos7 \
   --provider=libvirt
   

3) DESPLEGAR AMBIENTE
=====================






A REQUISITOS DE LA PC
=====================
- Procesador Intel con Procesador I5 o equivalente en AMD
- 8GB en RAM minimo.
- Puerto RJ45 y/o WIFI
- Disco duro de 100GB minimo.


1 OBTENER ISO DE CENTOS 7 64 BITS
=================================

Se  debe  descargar  la imagen  ISO  de  Centos  7  se recomienda  la  siguiente
pagina:  http://isoredirect.centos.org/centos/7/isos/x86_64/,   la  imagen  mide
aproximadamente 4.7 GB.

Se puede descargar en una PC con windows o linux.

2 GRABAR LA IMAGEN ISO EN UN USB PENDRIVE
=========================================

Una vez descargada  la imagen ISO es  necesario grabarla en una  memoria USB, se
requiere  con  capacidad  de  8GB  minimo.  Se  recomiendan  dos  procedimientos
posibles, uno  para Sistema  operativo Windows y  otro para  Sistemas Operativos
Linux.

- Windows

a) Download and install the latest version of Win32 Disk Imager
  https://sourceforge.net/projects/win32diskimager/?source=typ_redirect
b) Run Win32 Disk Imager.
c) Put the location of CentOS image into Image File text area. Win32 Disk Imager
can accept CentOS 7 *.iso file. No need to convert *.iso file to *.img file.
d) Choose your USB drive that you will bootable CentOS 7 as the Device.
e) Click button Write to start creating bootable USB drive.
f) When finished,  boot the desired pc  that you want to install  CentOS 7. Make
sure the created bootable USB drive is already attached to the desired pc.

- Linux

a) Conectar  una USB  drive al  sistema y  ejecutar el  comando "dmesg".  Un log
detallado con todos los eventos recientes se mostrara. se debe buscar una salida
parecida a la siguiente:

sd 6:0:0:0: Attached scsi generic sg3 type 0
sd 6:0:0:0: [sdc] 60481536 512-byte logical blocks: (31.0 GB/28.8 GiB)

Notar el nombre del dispositivo conectado - en el ejemplo anterior este es sdc.

b) Log in como root:

$ su -

Proporcionar el password cueando sea solicitado.

c)  Asegurarse que  el dispositivo  no este  montado. Primero,  usar el  comando
"findmnt  device"  y  el  nombre   del  dispositivo  que  encontraste  en  pasos
anteriores, por ejemplo  si el nombre del dispositivo es  sdc, usar el siguiente
comando:

# findmnt /dev/sdc

Si el comando no despliega salida, tu  puedes proceder con el siguiente paso, no
obstante si el comando muestra salida esta puede ser como la siguiente:

# findmnt /dev/sdc
TARGET  SOURCE   FSTYPE   OPTIONS
/mnt/iso /dev/sdb  iso9660 ro,relatime.


Notar  la  columna  TARGET,  Siguiente  usar el  comando  "umount  target"  para
desmontar el dispositivo:

# umount /mnt/iso


d) usar  el comando dd  para escribir el archivo  de imagen ISO  directamente al
dispositivo USB:

# dd if=/image_directory/image.iso of=/dev/device bs=blocksize

Ejemplo:

# dd if=/home/testuser/Downloads/rhel-server-7-x86_64-boot.iso of=/dev/sdb bs=512k

e)  Esperar a  que  el  comando "dd"  finalize  de escrib  ir  la  imagen en  el
dispositivo,  Notar que  no  hay  una barra  de  progreso:  la transferencia  es
finalizada  cuando el  indicador #,  se muestre  nuevamente. Despues  de que  el
indicador es  desplegado, log  out de  la cuenta  de root  y desconectar  el USB
drive.

3 INSTALAR CENTOS 7 EN UNA PC
=============================

NOTA: Es necesario que las extensiones de virtualizacion esten Activas en las PC
donde se instalara CentOS, esto se hace desde el BIOS del sistema

En la siguiente URL se muestra un ejemplo de como hacer dicho proceso:
https://docs.fedoraproject.org/en-US/Fedora/13/html/Virtualization_Guide/sect-Virtualization-Troubleshooting-Enabling_Intel_VT_and_AMD_V_virtualization_hardware_extensions_in_BIOS.html

Una vez hecho lo anterior, proceder con los siguientes pasos:

a) Conectar la USB Drive a un puerto de la PC e iniciarla.
b) Presionar la tecla para tener acceso al menu de arranque.
c) Seleccionar USB Drive y presionar ENTER.
d) En el menu "Centos 7" seleccione la opcion "Install Centos 7" y presione ENTER
e)  En   la  Ventana  "Resumen   de  la  Instalacion",  revisar   las siguientes
configuraciones:

  1) FECHA Y HORA: Configuradas en America/Ciudad de Mexico.
  2) SELECCION DE SOFTWARE: Servidor con GUI
  3) DESTINO DE LA INSTALACION: Seleccionar el Disco Duro de la PC.
     Seleccionar: "Voy a Configurar las particiones"
     Presioanr el link "Haga click para crearlos automaticamente"
     Pocicionarse en la particion "/home" y presionar el boton "-" para borrarla
     Revisar que solo queden las siguientes particiones:
     - /boot
     - /
     - swap
     NOTA Revisar que "/home" no exista.

  4) Presionar el boton "Listo"
f) RED & NOMBRE DE EQUIPO: 
  1)    Nombre   de    host:    Prover    un    nombre    como    por    ejemplo
"station1.labansible.ctt.com" y presionar el boton "apply"
  2) Sobre la Tarjeta de Red WIFI o la Ethernet, presionar el boton de Encendido
  0 | 1.
  3) Presionar el boton "Listo"

g) Presionar el boton "Empezar instalacion".

h) Presionar sobre "CONTRASEÑA DE ROOT" Y configurarla en centos 

i) Esperar a que termine de realizarse la instalacion.


Una vez que se concluye la instalacion, se presiona sobre el boton "Reiniciar",
el sistema reiniciara. Se debe presionar sobre "LICENCE INFORMATION" y  activar
"Acepto  el  acuerdo  de  licencia",  presionar  el  boton  "Listo" y presionar
"FINALIZAR INSTALACION".


PASOS POST-INSTALACION
======================

Una vez hecha la instalacion. Revisar:

1)  Que la  PC  tenga  salida a  internet,  en caso  de  no  tenerla revisar  la
configuracion de red, se puede acceder en el icono de red ubicado en la barra de
menus, en la parte superior del escritorio.

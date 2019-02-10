# nfs
## Crear recursos compartidos
Instalación de paquetes:
```
sudo apt install nfs-kernel-server
```
Crear carpeta compartida:
```
mkdir /srv/nfs
```
### Configurar carpetas compartidas en /etc/exports
Carpeta compartida para todo el mundo:
```
/srv/nfs/ *(rw,sync,no_root_squash)
```
Hacer que una subcarpeta no sea accesible
```
/srv/nfs/subcarpeta *(noaccess)
```
Carpeta compartida solo con una IP:
```
/srv/nfs/ 10.0.0.1(rw,sync,no_root_squash)
```
Otras opciones interesantes son: 

* ro sólo lectura
* rw lectura / escritura
* anonuid uid para el usuario anónimo (por ejemplo, anonuid = 2015) 
* /compartido 192.168.7.12 (rw, all_squash, anonuid_2015, no_subtree_check) esto quiere decir que
el usuario del equipo con IP .12 aparecerá con una uid = 2015 y el resto con nobody uid =
65534 que es por defecto como lo dice el sistema en passwd se puede cambiar el nombre de nobody
por anónimo por ejemplo.
* anongid gid para el usuario anónimo
* all_squash reemplaza el uid los usuario por un anónimo en ficheros creados
* no_all_squash los archivos creados aparecen con el uid del usuario
* root_squash reemplaza el uid de root por un anónimo en ficheros creados

Reiniciamos el servicio:
```
sudo systemctl restart nfs-kernel-server.service
```
Comprobamos que ha arrancado bien:
```
sudo systemctl status nfs-kernel-server.service
```
## Montar recurso compartido en Linux
Para montar el recurso compartido en el sistema de archivos del SO:
Crear el punto de montaje:
```
mkdir /mnt/nfs
```
Montar el recurso:
```
sudo mount IPdelServidor:/srv/nfs/ /mnt/nfs
```
Automontaje del recurso con el arranque de sistema
Editar el archivo /etc/fstab y agregar al final:
```
IPdelServidor:/srv/nfs  /mnt/nfs/ nfs rsize=8192,wsize=8192,timeo=14,intr
```
Por último reiniciar el ordenador

## Crear unidad de red en Windows
Agregar el rol cliente de NFS.

Montar la unidad de red por consola
```
mount IPdelServidor:/nombreunidad b:
```

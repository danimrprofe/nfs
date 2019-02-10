# nfs
Instalación de paquetes:
```
sudo apt install nfs-kernel-server
```
Crear carpeta compartida:
```
mkdir /srv/nfs
```
Configurar carpetas compartidas en /etc/exports
```
/srv/nfs/ *(rw,sync,no_root_squash)
```
Reiniciamos el servicio:
```
sudo systemctl restart nfs-kernel-server.service
```
Comprobamos que ha arrancado bien:
```
sudo systemctl status nfs-kernel-server.service
```
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

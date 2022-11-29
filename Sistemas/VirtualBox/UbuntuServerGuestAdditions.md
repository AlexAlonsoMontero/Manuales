# Instalar Guest additions:

* En dispositivo seleccionamos la opción VirtualBox: Dispositivos / insertar imagen de CD de las “Guest Additions“…

* Montamos en la carpeta mnt la imagen:
```
sudo mount /dev/cdrom /mnt
```
* Listamos el directorio: 
```
ls /mnt
```
* Nos asegturamos que están instaladas todas las dependencias:
```
sudo apt-get install -y dkms build-essential linux-headers-generic linux-headers-$(uname -r)
```
* Nos logamos como administradores y montamos las Guest Additions
```
sudo su
cd /mnt
./VBoxLinuxAdditions.run
```

# Cambiar resolución de pantalla

* Abrir con tu editor favorito  "/etc/default/grub" y añadir o modificar las siguientes líneas.
```
GRUB_GFXMODE=1024x768
GRUB_CMDLINE_LINUX_DEFAULT="nomodeset"
GRUB_GFXPAYLOAD_LINUX=keep
```
** Importante GRUB_GFXMODE= poner una resolución que aguante tu tarjeta gŕafica
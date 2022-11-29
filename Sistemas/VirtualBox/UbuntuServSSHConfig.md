# Configuración de ssh en Ubuntu
* En caso de que no hayamos intalado ssh al instlar el sistema operativo
```
sudo apt install openssh-server
```
* Verificar estado de ssh
```
sudo systemctl status ssh
```
* Debemos ver algo así:

<kbd>
    <img src="./imagenes/ubuntu-ssh-runing.png">
</kbd>


* Si el servidor sigue inactivo:
```
sudo systemctl enable ssh
sudo systemctl start ssh
```

*  Fichero de configuración: sudo nano "/etc/ssh/sshd_config"
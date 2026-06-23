# Tarea 1

#### parte a

 
> sudo apt install openssh-server

> Cambiar a un puerto diferente del 22 -> 4848

> Maximo intento de contrasenia a 2 -> MaxAuthTries


#### parte b

> mkdir usuarios
> cd usuarios
> mkdir administracion

##### Grupo
> groupadd programadores

##### Permisos
> sudo chmod 754 /usuarios/administracion

// Root
> setfacl -d -m u:root:rwx usuarios/administracion/

// Programadores
> setfacl -d -m g:programadores:wx usuarios/administracion/

// otros
> setfacl -d -m o:r usuarios/administracion/

##### Parte c

#### Seccion de backup
> mkdir backup
> nano backup.sh


##### Script del backup
```bash
SHELL=/bin/bash
now=$(date)

cp -r /usuarios/administracion/ "/backup/$now"
```

# Crontab
> 00 23 * * * backup.sh


# Samba
```
root@AdminPET:~# sudo nano /etc/samba/smb.conf
```

```
[compartidos]
   guest ok = yes
   path = /usuarios/administracion
   writeable = yes
   browsable = yes
   reate mask = 0754

```


```
root@AdminPET:~# sudo chgrp -R programadores /usuarios/administracion
root@AdminPET:~# sudo chmod 2770 /usuarios/administracion
root@AdminPET:~# smbd
```


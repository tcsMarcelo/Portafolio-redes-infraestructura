# __Configuración básica de usuarios / acceso por SSH__ #

<img width="450" height="450" alt="1" src="https://github.com/user-attachments/assets/5ddbdd55-17c3-47c9-a073-62521d60f7d5" />

1. Configuración del Switch.

En modo de configuración global se asigna los primeros parámetros básicos
  ```cisco
  - hostname "nombre.del.dispositivo"
  - ip domain-name "nombre.de.dominio"
  - line console 0 
      - password "contraseña.de.la.consola"
      - login
  - enable secret "contraseña.modo.privilegiado"
  - banner motd #mensaje.del.dispositivo#
```
Luego, los respectivos comandos de acceso SSH
```cisco
  - ip domain-name "nombre.de.dominio"
  - cryto key-generate rsa
          1024
  - ip ssh version 2
  - line vty 0 5 (IMPORTANTE: En el ejemplo solo estarán permitidos 6 usuarios simultáneos)
      - login authentication default
      - transport input ssh
```

2. Configuración del servidor
   En el servidor se debe asignar la dirección IP correspondiente a la red LAN,
   esta se debe configurar en el SWITCH para que los usuarios puedan autenticarse
   por medio del servidor.

   En la pestaña "SERVICIOS" > "AAA", se debe configurar lo siguiente:
     - Dirección IP del cliente (Dirección del SWITCH)
     - Nombre del cliente (SWITCH)
     - Password (Secret) 

   Más abajo ir agregando los usuarios que se autenticarán en el servidor.
     - Nombre
     - Contraseña
       

### __Configuración básica de usuarios / acceso por SSH / Autenticación en el servidor__ ###

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
  - service password-encryption
```
Luego, los respectivos comandos de acceso SSH
```cisco
  - ip domain-name "nombre.de.dominio"
  - interface vlan 1
      - ip address "dirección/máscara
      - no shutdown
  - cryto key-generate rsa
          1024
  - ip ssh version 2
  - line vty 0 5 (IMPORTANTE: En el ejemplo solo estarán permitidos 6 usuarios simultáneos)
      - login authentication default
      - transport input ssh
  - copy running-config startup-config
```
<img width="513" height="450" alt="8" src="https://github.com/user-attachments/assets/4d3816ab-61dd-425b-9830-91486c564c84" />

Vamos a continuar con los comandos de autenticación para el servidor TACACS+
```cisco
  - aaa new-model
  - aaa authentication login default group tacacs+ enable
  - tacacs-server host "dirección.servidor"
  - tacacs-server key "clave.creada.en.servidor"
```
2. Configuración de la dirección IP en los PC
   En cada uno de los dispositivos se asignará un dirección IPV4 estática, esto con fines prácticos.
   En una topología de red en donde se conectarán más equipos, se suele asignar un direccionamiento
   automático por medio de un servidor DHCP.

  - En pestaña "DESKTOP", se debe acceder al apartado "IP CONFIGURATION" y asignar la IP correspondiente
  a la red LAN con la cuál estamos trabajando, también agregar la máscara de red.

NOTA: Para hacer pruebas de conectividad entre dispositivos se ocupa en comando "ping" más la
dirección IP del equipo a donde queremos conectarnos.
   
<img width="450" height="450" alt="6" src="https://github.com/user-attachments/assets/f62ef673-c7fc-43f2-bf26-da01e0cdc15b" />


4. Configuración del servidor
   En el servidor se debe asignar la dirección IP correspondiente a la red LAN,
   esta se debe configurar luego en el SWITCH para que los usuarios puedan autenticarse
   en el servidor.

   En la pestaña "SERVICIOS" > "AAA", se debe configurar lo siguiente:
     - Dirección IP del cliente (Dirección del SWITCH)
     - Nombre del cliente (SWITCH)
     - Password (Secret) 

   Más abajo ir agregando los usuarios que se autenticarán en el servidor.
     - Nombre
     - Contraseña
       


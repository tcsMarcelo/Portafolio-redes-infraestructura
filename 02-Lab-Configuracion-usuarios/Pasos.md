# Configuración básica de usuarios #

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
  - ip domain-name "nombre.de.dominio"
  - cryto key-generate rsa
          1024
  - ip ssh version 2
  - line vty 0 5 (IMPORTANTE: En el ejemplo, solo estarán permitidos 6 usuarios simultáneos)
      - login authentication default
      - transport input ssh






2. Configuración del servidor
3. 

### Configuración básica de un Switch Cisco 2960 y acceso por SSH ###

A continuación se muestran los parámetros básicos de configuración de un Switch Cisco 2960, se debe considerar
que para poder acceder al dispositivo se debe hacer uso de un cable RS232 el cuál irá conectado
al puerto de consola del SWITCH.

<img width="450" height="450" alt="1" src="https://github.com/user-attachments/assets/ed36b304-f2a1-40e2-961f-6dad251057ab" />


1- En modo de configuración global: 
```cisco
  - hostname "nombre.del.dispositivo"
  - line console 0
      password "contraseña.de.consola"
      login
  - enable secret "CONTRASEÑA" (MCG: clave de acceso al modo privilegiado).
  - service password-encryption (MCG: encripta las contraseñas).
  - banner motd #MENSAJE# (MCG: crea un mensaje en el dispositivo).
  - username "NOMBRE_USUARIO" secret "CONTRASEÑA" (MCG).
  - ip domain-name "NOMBRE_DOMINIO" (MCG).
```

    
2. Configuración de la interfaz VLAN 1
```cisco
  - interface vlan 1 (MCG) (VLAN por defecto).
      ip address "DIRECCIÓN / MÁSCARA".
      no shutdown
```
    
3. Generación de claves RSA
```cisco
  - crypto key generate rsa (consultar opción general con ?).
  - 1024 MB (el mínimo recomendado)
```
    
4. Activación del protocolo SSH
```cisco
  - ip ssh version 2
  - line vty 0 15
      login local
      transport input ssh
```
    
5. Guardar la configuración
```cisco
  - copy running-config startup-config
```

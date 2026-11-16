# Configuración básica de un Switch Cisco 2960
A continuación se muestran los parámetros básicos de configuración de un Switch Cisco 2960

1- En modo de configuración global: 
  - hostname "nombre.del.dispositivo"
  - line console 0
    password "contraseña.de.consola"
    login
  - enable secret "CONTRASEÑA" (MCG: clave de acceso al modo privilegiado).
  - service password-encryption (MCG: encripta las contraseñas).
  - banner motd #MENSAJE# (MCG: crea un mensaje en el dispositivo).
  - username "NOMBRE_USUARIO" secret "CONTRASEÑA" (MCG).
  - ip domain-name "NOMBRE_DOMINIO" (MCG).
    
2. Configuración de la interfaz VLAN 1
  - interface vlan 1 (MCG) (VLAN por defecto).
      ip address "DIRECCIÓN / MÁSCARA".
      no shutdown
    
3. Generación de claves RSA
  - crypto key generate rsa (consultar opción general con ?).
  - 1024 MB (el mínimo recomendado)
    
4. Activación del protocolo SSH
  - ip ssh version 2
  - line vty 0 15
      login local
      transport input ssh
    
5. Guardar la configuración
  - copy running-config startup-config

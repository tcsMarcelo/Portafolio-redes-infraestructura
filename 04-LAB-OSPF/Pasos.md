### Enrutamiento dinámico por medio de OSPF ###
<img width="628" height="450" alt="1" src="https://github.com/user-attachments/assets/e7d5801e-cb4b-49e8-9e40-3f1807ab9a66" />


En cada router (config. Global):

```cisco
- router ospf "número de proceso"
      - router-id "número identificador del router" (Ej: 0.0.0.1)
      - network "IP-RED" + "WILDCARD" + area "número de área" 
```

Autenticación mediante tres métodos diferentes, el primero de ellos es el menos seguro ya que la contraseña viaja
sin cifrar, el otro método por cifrado MD5 y por último el más recomendado SHA-256.

En la interfaz de salida, ingresar el siguiente comando:
```cisco
- ip ospf authentication 
- ip ospf authentication-key "PASSWORD"
```
El segundo método se habilita en la interfaz de salida:
```cisco
- ip ospf authentication message-digest
- ip ospf message-digest-key 1 md5 "PASSWORD"
```
Por último el tercer método de autenticación, esta vez se debe ingresar en el modo configuración global:
```cisco
- key chain "NOMBRE-KEY" key 1 key-string "PASSWORD" cryptographic-algorithm hmac-sha-256 
```
Luego, en la interfaz de salida:
```cisco
- ip ospf authentication key-chain "NOMBRE-KEY"
```

NOTA: Las pruebas hechas en laboratorios anteriores arrojaron nula comunicación entre dispositivos, por lo que 
tardé un tiempo en encontrar la solución. Finalmente me di cuenta que había olvidado añadir las redes LAN de los 
otros enrutadores.

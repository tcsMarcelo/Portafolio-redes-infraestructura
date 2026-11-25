### Enrutamiento dinámico por medio de OSPF ###
<img width="628" height="450" alt="1" src="https://github.com/user-attachments/assets/e7d5801e-cb4b-49e8-9e40-3f1807ab9a66" />

1. Establecer OSPF en los enrutadores:

Para configurar OSPF en cada ROUTER de la topología mostrada en la imagen de más arriba, es necesario entrar
al modo de configuración global e ingresar los siguientes comandos:

```cisco
- router ospf "número de proceso"
      - router-id "número identificador del router" (Ej: 0.0.0.1)
      - network "IP-RED" + "WILDCARD" + area "número de área" 
```
<img width="450" height="450" alt="serialAD3" src="https://github.com/user-attachments/assets/7449d2ea-3caf-4003-9fcb-95f6c266aa8a" />
<img width="450" height="450" alt="serialAD2" src="https://github.com/user-attachments/assets/0adb20f7-8d9e-42ac-959d-f7fe5f9847c9" />
<img width="450" height="450" alt="serialAD1" src="https://github.com/user-attachments/assets/bcc30fa2-74af-4c5c-bc2a-edcbdbc346de" />


NOTA: Las pruebas hechas en laboratorios anteriores arrojaron nula comunicación entre dispositivos, por lo que 
tardé un tiempo en encontrar la solución. Finalmente me di cuenta que había olvidado añadir las redes LAN de los 
otros enrutadores.

2. Establecer la autenticación:

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



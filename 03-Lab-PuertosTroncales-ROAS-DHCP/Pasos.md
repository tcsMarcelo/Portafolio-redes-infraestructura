### Comunicación inter VLAN, ROUTER ON A STICK y asignación de direcciones por DHCP ###

<img width="524" height="450" alt="1" src="https://github.com/user-attachments/assets/855f1649-4ade-4822-937e-6c9ebc73d190" />


1. Configuraciones del SWITCH (SW)

Después de haber accedido al switch mediante el cable de consola, haber ingresado los comandos de configuración básicos
y de acceso por SSH, se crean las correspondientes VLAN que participarán en la comunicación. Este ejercicio muestra
cómo algunas de las interfaces serán movidas a una nueva VLAN por motivos de seguridad ya que por defecto y cómo se sabe todas 
los puertos están asignados a la VLAN 1.

En el modo de configuración global: 
```cisco
- vlan "número de vlan"
- name "nombre de vlan"
```

Dentro del mismo modo, asignar el rango de interfaces a las VLAN creadas. 

```cisco
- interface f0/1 switchport mode access 
- switchport access vlan 10
- spanning-tree portfast
```
<img width="628" height="450" alt="3" src="https://github.com/user-attachments/assets/645f7d63-a8e1-402b-ac53-b881a088ee54" />


Definir los puertos troncales a una interfaz, los puertos de salida que apuntan al ROUTER y al otro SWITCH se establecen cómo 
puertos troncales ya que por ellos viajarán cada una de las VLAN:

<img width="450" height="450" alt="7" src="https://github.com/user-attachments/assets/f6fd551b-26c8-4ca2-9e5a-23a7ac1bd42d" />


```cisco
- interface g0/1
- switchport mode trunk
- switchport trunk allowed vlan "número de vlan"
- switchport trunk native vlan "número de vlan nativa"
```

2. Configuración del ROUTER.

Para evitar pasos extra en mi ejemplo, accedo directamente al ROUTER para ingresar los comandos esenciales. Tengo muy presente
que en entornos de producción es relevante asignar los comandos de configuración básicos cómo el nombre del dispositivo, mensaje
de ROUTER, contraseñas, encriptación de contraseñas, etc.  


Configurar subinterfaces (ejemplo: G0/0.10):
```cisco
- interface g0/0.10
- encapsulation dot1Q "número de VLAN"
- ip address "dirección IP/máscara"
```
Levantar puerto de salida al switch desde el modo de configuración global:

```cisco
- interface g0/0
- no shutdown
```
	
Lo que sigue es crear el pool de direcciones que alimentarán a las VLAN y excluir aquellas direcciones que deseamos 
que no sean tomadas en cuenta. En modo de configuración global:

```cisco
- ip dhcp excluded-address "rango de direcciones a excluir"
- ip dhcp pool "nombre del pool"
  - network "IP-red"
  - default-router "IP puerta de enlace"
```
3. ESTABLECER DIRECCIÓN IP EN LOS DISPOSITIVOS UTILIZANDO DHCP.

En cada dispositivo se debe acceder al apartado "Dirección IP"

ANOTACIÓN: Se debe levantar la interfaz física para que levanten las subinterfaces lógicas.


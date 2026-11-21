### Comunicación inter VLAN, ROUTER ON A STICK y asignación de direcciones por DHCP ###

<img width="524" height="450" alt="1" src="https://github.com/user-attachments/assets/855f1649-4ade-4822-937e-6c9ebc73d190" />


1. Configuraciones del SWITCH (SW)

Después de haber accedido al switch mediante el cable de consola, haber ingresado los comandos de configuración básicos
y de acceso por SSH, se crean las correspondientes VLAN que participarán en la comunicación. Este ejercicio muestra
cómo algunas de las interfaces son movidas a otra VLAN por motivos de seguridad. 

En el modo de configuración global: 
```cisco
- vlan "número de vlan"
- name "nombre de vlan"
```

Dentro del mismo modo asignar el rango de interfaces a las VLAN creadas. 

```cisco
- interface f0/1 switchport mode access 
- switchport access vlan 10
- spanning-tree portfast
```

Asignar puerto troncal a una interfaz, los puertos de salida que apuntan al ROUTER y al otro SWITCH se establecen cómo 
puertos troncales ya que por ellos viajarán cada una de las VLAN:

<img width="450" height="450" alt="7" src="https://github.com/user-attachments/assets/f6fd551b-26c8-4ca2-9e5a-23a7ac1bd42d" />


```cisco
- interface g0/1
- switchport mode trunk(Dependerá del tipo de switch).
- switchport trunk allowed vlan (agregar VLAN permitidas).
- switchport trunk native vlan (VLAN nativa)
```

2. EN EL ROUTER:Levantar puerto de salida al switch (no shutdown):

```cisco
- interface g0/0
- no shutdown
```
Configurar subinterfaces (ejemplo: G0/0.10):
```cisco
- interface g0/0.10
- encapsulation dot1Q 10 (indicar N.º de VLAN)
- ip address "dirección IP/máscara"
```
	
En modo de configuración global:
```cisco
- ip dhcp excluded-address "rango IP"
- ip dhcp pool VLAN_10(El nombre lo asigna uno como administrador).
  - network "IP-red"
  - default-router "IP puerta de enlace"
```
3. ESTABLECER DIRECCIÓN IP EN LOS DISPOSITIVOS UTILIZANDO DHCP.

ANOTACIÓN: Se debe levantar la interfaz física para que levanten las subinterfaces lógicas.


Universidad de San Carlos de Guetamala  
Facultad de Ingenieria  
Escuela de Ciencias y Sistemas  
Redes de computadoras 2  

| Nombre    | Carnet   |
| --------- | -------- |
| Esdras Toc     | 201807373 |
| Brian Erazo    | 201807253 |
| Brayan Mejia   | 201900576 |


#Tipologia
![Topologia](Capturas/Topologia.jpg)

# VLANS
| VLAN | NUMERO  |
| --------- | --------- |
| VLAN A    |           |
| VLAN B    |           |
| VLAN C    |           |
| VLAN D    |           |


# DIRECCION IP PC

| Departamento | Direccion IP | Mascara |
| --------- | --------- | --------- |
| CORPORATIVO    | 192.168.88.3    | 255.255.255.0    |
| CORPORATIVO    | 192.168.88.2    | 255.255.255.0    |
| SOPORTE    | 192.168.78.2    | 255.255.255.0    |
| RRHH    | 192.168.68.2    | 255.255.255.0    |
| RRHH   | 192.168.68.3    | 255.255.255.0   |
| RRHH    | 192.168.68.4    | 255.255.255.0   |

# CONFIGURACION LADO IZQUIERDO

## SW1
```
en
conf t
vlan 68
name CORPORATIVO68

int vlan 68
ip address 192.168.68.1 255.255.255.0
no shut
exit

interface range FastEthernet0/1 - 2
channel-group 1 mode active

```

## MSW1
```
en
conf t
vlan 68
name CORPORATIVO68
exit
vlan 18
name VENTAS18
exit

int vlan 68
ip address 192.168.68.1 255.255.255.0
no shut
exit

ip routing
interface vlan 18
ip address 1.0.0.2 255.0.0.0
no shutdown
exit

router eigrp 1
network 1.0.0.0
exit
do write

```

## Configuracion  SW1 - MSW1

### Configuracion SW1

```
enable
configure terminal
interface range FastEthernet0/1 - 2
channel-group 1 mode active

```

### Configuracion MSW1 LACP
```

enable
configure terminal
interface range FastEthernet0/1 - 2  
channel-group 1 mode active 


```

En ambos switches debemos de crear el enlace con Ethernetchanel con el mismo numero que se espesifico en los comandos anteriores  

```

interface Port-channel 1

```
En ambos switches, puedes verificar la configuración y el estado del grupo EtherChannel con comandos como show etherchannel summary o show etherchannel port-channel. 


# CONFIGURACION CENTRO

## SW2
```
en
conf t
vlan 68
name CORPORATIVO68

int vlan 68
ip address 192.168.78.1 255.255.255.0
no shut
exit

```

## MSW4
```
enable
conf t

vlan 68
name CORPORATIVO68
exit
vlan 28
name DISTRIBUCIÓN28
exit
vlan 18
name VENTAS18
exit

ip routing
interface vlan 18
ip address 1.0.0.1 255.0.0.0
no shutdown
exit

router eigrp 1
network 1.0.0.0
exit
do write

```

## Configuracion  SW2 - MSW4 LACP

### Configuracion SW2

```
enable
configure terminal
interface range FastEthernet0/1 - 2
channel-group 3 mode active


```

### Configuracion MSW4
```

enable
configure terminal
interface range FastEthernet0/1 - 2
channel-group 3 mode active



```

En ambos switches debemos de crear el enlace con Ethernetchanel con el mismo numero que se espesifico en los comandos anteriores  

```

interface Port-channel 3


```
En ambos switches, puedes verificar la configuración y el estado del grupo EtherChannel con comandos como show etherchannel summary o show etherchannel port-channel. 


# CONFIGURACION LADO DERECHO

## SW3
```
en
conf t
vlan 68
name CORPORATIVO68

int vlan 68
ip address 192.168.88.1 255.255.255.0
no shut
exit
```

## MSW7
```
en
conf t
vlan 68
name CORPORATIVO68

int vlan 68
ip address 192.168.68.1 255.255.255.0
no shut
exit

```

# CONFIGURACION PARA OSPF

## Para el MSW4

enable  
conf t  

vlan 68  
name CORPORATIVO68  
exit  
vlan 28  
name DISTRIBUCIÓN28  
exit  
vlan 18  
name VENTAS18  
exit  

interface FastEthernet0/4  
no switchport  
ip address 2.0.0.1 255.255.255.0  
no shutdown  
exit  

router ospf 1  
network 2.0.0.0 0.0.0.255 area 0  
exit  
do write  


## Para el MSW7

enable  
conf t  

vlan 68  
name CORPORATIVO68  
exit  
vlan 28  
name DISTRIBUCIÓN28  
exit  
vlan 18  
name VENTAS18  
exit  

interface FastEthernet0/4  
no switchport  
ip address 2.0.0.2 255.255.255.0  
no shutdown  
exit  

ip routing  
router ospf 1  
network 2.0.0.0 0.0.0.255 area 0  
exit  
do write  



## Configuracion  SW3 - MSW7 LACP

### Configuracion SW3

```
enable
configure terminal
interface range FastEthernet0/1 - 2
channel-group 2 mode active


```

### Configuracion MSW1
```

enable
configure terminal
interface range FastEthernet0/1 - 2
channel-group 2 mode active



```

En ambos switches debemos de crear el enlace con Ethernetchanel con el mismo numero que se espesifico en los comandos anteriores  

```

interface Port-channel 2


```
En ambos switches, puedes verificar la configuración y el estado del grupo EtherChannel con comandos como show etherchannel summary o show etherchannel port-channel. 





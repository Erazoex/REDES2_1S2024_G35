# CONFIGURACION PARA EIGRP

## Para el switch 4
```
enable
conf t

vlan 60
name CORPORATIVO68
exit
vlan 20
name DISTRIBUCIÓN28
exit
vlan 10
name VENTAS18
exit

ip routing
interface vlan 10
ip address 1.0.0.1 255.0.0.0
no shutdown
exit

router eigrp 1
network 1.0.0.0
exit
do write
```

## Para el switch 1
```
enable
conf t

ip routing
interface vlan 10
ip address 1.0.0.2 255.0.0.0
no shutdown
exit

router eigrp 1
network 1.0.0.0
exit
do write

```

# CONFIGURACION PARA OSPF

## Para el MSW4

enable
conf t

vlan 60
name CORPORATIVO68
exit
vlan 20
name DISTRIBUCIÓN28
exit
vlan 10
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

vlan 60
name CORPORATIVO68
exit
vlan 20
name DISTRIBUCIÓN28
exit
vlan 10
name VENTAS18
exit

interface FastEthernet0/4
no switchport
ip address 2.0.0.2 255.255.255.0
no shutdown
exit

router ospf 1
network 2.0.0.0 0.0.0.255 area 0
exit
do write





# CONFIGURACION LACP 

## Configuracion  SW1 - MSW1

### Configuracion SW1

```
enable
configure terminal
interface range FastEthernet0/1 - 2
channel-group 1 mode active

```

### Configuracion MSW1
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


## Configuracion  SW3 - MSW7

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



## Configuracion  SW2 - MSW4

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
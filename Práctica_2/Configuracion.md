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
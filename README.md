# CCNA-Réseau-TP

## Config des switchs : 

### R1 :

    interface FastEthernet0/0
     ip address dhcp
     ip nat outside
     ip virtual-reassembly
     duplex auto
     speed auto
    !
    interface FastEthernet0/1
     no ip address
     duplex auto
     speed auto
    !
    interface FastEthernet0/1.30
     encapsulation dot1Q 30
     ip address 10.5.30.254 255.255.255.0
     ip nat inside
     ip virtual-reassembly
    !
    interface FastEthernet1/0
     no ip address
     duplex auto
     speed auto
    !
    interface FastEthernet1/0.10
     encapsulation dot1Q 10
     ip address 10.5.10.254 255.255.255.0
     ip nat inside
     ip virtual-reassembly
    !
    interface FastEthernet1/0.20
     encapsulation dot1Q 20
     ip address 10.5.20.254 255.255.255.0
     ip nat inside
     ip virtual-reassembly

### client-sw1 : 

    interface Ethernet0/0
     switchport trunk encapsulation dot1q
     switchport mode trunk
    !
    interface Ethernet0/1
     switchport access vlan 10
     switchport mode access
    !
    interface Ethernet0/2
     switchport access vlan 20
     switchport mode access
    !
### client-sw2 : 

    interface Ethernet0/0
     switchport trunk encapsulation dot1q
     switchport mode trunk
    !
    interface Ethernet0/1
     switchport trunk encapsulation dot1q
     switchport mode trunk
    !
    interface Ethernet0/2
     switchport trunk encapsulation dot1q
     switchport mode trunk
    !
    interface Ethernet0/3
     switchport access vlan 10
     switchport mode access
    !
    interface Ethernet1/0
     switchport access vlan 20
     switchport mode access
    !
### client-sw3 : 


    interface Ethernet0/0
     switchport trunk encapsulation dot1q
     switchport mode trunk
    !
    interface Ethernet0/1
     switchport access vlan 10
     switchport mode access
    !
    interface Ethernet0/2
     switchport access vlan 20
     switchport mode access
    !
    interface Ethernet0/3
     switchport access vlan 30
     switchport mode access
    !
### infra-sw1 :

    interface Ethernet0/0
     switchport trunk encapsulation dot1q
     switchport mode trunk
    !
    interface Ethernet0/1
     switchport access vlan 30
     switchport mode access
    !
    interface Ethernet0/2
     switchport access vlan 30
     switchport mode access
    !

Après j'ai les mêmes fichiers de config que tu à donner donc bon....

## TP : Métrologie Réseau : SNMP, monitoring, gestion de logs

### 1. Installation

#### Les répos : 
```
yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
yum install http://yum.opennms.org/repofiles/opennms-repo-stable-rhel7.noarch.rpm
yum install http://rpms.remirepo.net/enterprise/remi-release-7.rpm
```

#### Les Packages : 

```
yum install yum-utils
```
```
yum-config-manager --enable remi-php72
```
```
yum update
```



<!--stackedit_data:
eyJoaXN0b3J5IjpbODk0MTUzNjI0XX0=
-->
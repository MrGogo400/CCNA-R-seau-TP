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



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTI1NzYxMjA2M119
-->
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
```
yum install wget.x86_64 httpd.x86_64 php.x86_64 php-opcache.x86_64 php-mysql.x86_64 php-gd.x86_64 \
            php-posix php-pear.noarch cronie.x86_64 net-snmp.x86_64 net-snmp-utils.x86_64 \
            fping.x86_64 mariadb-server.x86_64 mariadb.x86_64 MySQL-python.x86_64 rrdtool.x86_64 \
            subversion.x86_64  jwhois.x86_64 ipmitool.x86_64 graphviz.x86_64 ImageMagick.x86_64 \
            php-sodium.x86_64
```

#### Installation de Observium :

```
mkdir -p /opt/observium && cd /opt
```
```
wget http://www.observium.org/observium-community-latest.tar.gz
tar zxvf observium-community-latest.tar.gz
```
### 2. Base de données :

```
systemctl enable mariadb
systemctl start mariadb
```

```
/usr/bin/mysqladmin -u root password 'afn'
```

```
mysql -u root -p
afn
mysql> CREATE DATABASE observium DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;
mysql> GRANT ALL PRIVILEGES ON observium.* TO 'observium'@'localhost' IDENTIFIED BY '<observium db password>';
mysql> exit;
```
### 3. Configuration de Observium :

```
cd observium
```
```
cp config.php.default config.php
```

> On oublie pas de changer les identifiants MySQL par les notres
```
./discovery.php -u
```

### 4. Configuration du système

### 4.1 FPing

> On rajoute cette ligne dans le fichier config.php de fping

```
$config['fping'] = "/sbin/fping";
```

### 4.2 SELinux

> On désactive SELinux pour le passer en permissive

```
setenforce 0
```

> Dans le fichier **/etc/selinux/config** on le passe en permissive
```
 SELINUX=permissive
```
### 4.3 RRD & Apache

```
 mkdir rrd
 chown apache:apache rrd
```

> Dans le fichier **/etc/httpd/conf.d/observium.conf** et on rajoute le VirtualHost

```
<VirtualHost *>
   DocumentRoot /opt/observium/html/
   ServerName  observium.domain.com
   CustomLog /opt/observium/logs/access_log combined
   ErrorLog /opt/observium/logs/error_log
   <Directory "/opt/observium/html/">
     AllowOverride All
     Options FollowSymLinks MultiViews
     Require all granted
   </Directory>
</VirtualHost>
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbOTQ5Nzg3MDQzLC00NTIxNjk1NDJdfQ==
-->
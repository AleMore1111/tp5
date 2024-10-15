# I. Setup

### ☀️ Uniquement avec des commandes, prouvez-que :
````
[askun@RouteurSSH ~]$ ip a
3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:7f:a8:40 brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.254/24 brd 10.5.1.255 scope global noprefixroute enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fe7f:a840/64 scope link
       valid_lft forever preferred_lft forever
````
````
[askun@rundown ~]$ ip a
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:82:db:45 brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.11/24 brd 10.5.1.255 scope global noprefixroute enp0s3
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fe82:db45/64 scope link
       valid_lft forever preferred_lft forever
````
````
[askun@Client2 ~]$ ip a
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:73:26:03 brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.12/24 brd 10.5.1.255 scope global noprefixroute enp0s3
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fe73:2603/64 scope link
       valid_lft forever preferred_lft forever
````
````
PS C:\Users\Moreaux> ping 10.5.1.11
Envoi d’une requête 'Ping'  10.5.1.11 avec 32 octets de données :
Réponse de 10.5.1.11 : octets=32 temps=1 ms TTL=64
Réponse de 10.5.1.11 : octets=32 temps=1 ms TTL=64
Réponse de 10.5.1.11 : octets=32 temps=2 ms TTL=64
Réponse de 10.5.1.11 : octets=32 temps=1 ms TTL=64
````
````
PS C:\Users\Moreaux> ping 10.5.1.12
Envoi d’une requête 'Ping'  10.5.1.12 avec 32 octets de données :
Réponse de 10.5.1.12 : octets=32 temps=4 ms TTL=64
Réponse de 10.5.1.12 : octets=32 temps=1 ms TTL=64
Réponse de 10.5.1.12 : octets=32 temps=1 ms TTL=64
Réponse de 10.5.1.12 : octets=32 temps=1 ms TTL=64
````
# II. Accès internet pour tous

## 1. Accès internet routeur

### ☀️ Déjà, prouvez que le routeur a un accès internet
````
[askun@RouteurSSH ~]$ ping www.ynov.com
PING www.ynov.com (172.67.74.226) 56(84) bytes of data.
64 bytes from 172.67.74.226 (172.67.74.226): icmp_seq=1 ttl=255 time=19.1 ms
64 bytes from 172.67.74.226 (172.67.74.226): icmp_seq=2 ttl=255 time=21.8 ms
64 bytes from 172.67.74.226 (172.67.74.226): icmp_seq=3 ttl=255 time=15.9 ms
64 bytes from 172.67.74.226 (172.67.74.226): icmp_seq=4 ttl=255 time=18.7 ms
64 bytes from 172.67.74.226 (172.67.74.226): icmp_seq=5 ttl=255 time=18.1 ms
````
### ☀️ **Activez le routage**
``````
[askun@RouteurSSH ~]$ sudo firewall-cmd --add-masquerade --permanent
success
``````
``````
[askun@RouteurSSH ~]$ sudo firewall-cmd --reload
success
``````
## 2. Accès internet clients
### ☀️ Prouvez que les clients ont un accès internet
````
[askun@rundown ~]$ ping www.ynov.com
PING www.ynov.com (172.67.74.226) 56(84) bytes of data.
64 bytes from 172.67.74.226 (172.67.74.226): icmp_seq=1 ttl=254 time=16.2 ms
64 bytes from 172.67.74.226 (172.67.74.226): icmp_seq=2 ttl=254 time=30.2 ms
64 bytes from 172.67.74.226 (172.67.74.226): icmp_seq=3 ttl=254 time=44.7 ms
64 bytes from 172.67.74.226 (172.67.74.226): icmp_seq=4 ttl=254 time=21.0 ms
64 bytes from 172.67.74.226 (172.67.74.226): icmp_seq=5 ttl=254 time=16.4 ms
^C
--- www.ynov.com ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4011ms
rtt min/avg/max/mdev = 16.168/25.677/44.682/10.768 ms
````
````
[askun@rundown ~]$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:82:db:45 brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.11/24 brd 10.5.1.255 scope global noprefixroute enp0s3
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fe82:db45/64 scope link  valid_lft forever preferred_lft forever
````



### ☀️ Montrez-moi le contenu final du fichier de configuration de l'interface réseau
````
[askun@Client2 ~]$  sudo cat /etc/sysconfig/network-scripts/ifcfg-enp0s3
[sudo] password for askun:
DEVICE=enp0s3
NAME=Clonepc2

ONBOOT=yes
BOOTPROTO=static

IPADDR=10.5.1.12
NETMASK=255.255.255.0
GATEWAY=10.5.1.254
DNS1=1.1.1.1
````

# III. Serveur SSH


### ☀️ Sur routeur.tp5.b1, déterminer sur quel port écoute le serveur SSH
````
[askun@RouteurSSH ~]$ sudo ss -lnpt | grep 22
LISTEN 0      128          0.0.0.0:22        0.0.0.0:*    users:(("sshd",pid=693,fd=3))
LISTEN 0      128             [::]:22           [::]:*    users:(("sshd",pid=693,fd=4))
````


### ☀️ Sur routeur.tp5.b1, vérifier que ce port est bien ouvert
````
[askun@RouteurSSH ~]$ sudo firewall-cmd --permanent --add-port=22/tcp
success
````

# IV. Serveur DHCP

## 3. Rendu attendu

☀️ **Installez et configurez un serveur DHCP sur la machine `routeur.tp5.b1`**
``````
[askun@RouteurSSH ~]$ sudo dnf install dhcp-server
``````
``````
[askun@RouteurSSH ~]$ sudo nano /etc/dhcp/dhcpd.conf
``````
``````
default-lease-time 2592000;

max-lease-time 3888000;

authoritative;

subnet 10.5.1.0 netmask 255.255.255.0 {
    range dynamic-bootp 10.5.1.137 10.5.1.237;
    option routers 10.5.1.254;
    option domain-name-servers 1.1.1.1;

}
```````
``````
[askun@RouteurSSH ~]$ sudo systemctl restart dhcpd
Oct 15 18:53:26 RouteurSSH dhcpd[1306]: Internet Systems Consortium DHCP Server 4.4.2b1
Oct 15 18:53:26 RouteurSSH dhcpd[1306]: Copyright 2004-2019 Internet Systems Consortium.
Oct 15 18:53:26 RouteurSSH dhcpd[1306]: All rights reserved.
Oct 15 18:53:26 RouteurSSH dhcpd[1306]: For info, please visit https://www.isc.org/software/dhcp/
Oct 15 18:53:26 RouteurSSH dhcpd[1306]: ldap_gssapi_principal is not set,GSSAPI Authentication for LDAP will not be used
Oct 15 18:53:26 RouteurSSH dhcpd[1306]: Not searching LDAP since ldap-server, ldap-port and ldap-base-dn were not specified in the config file
Oct 15 18:53:26 RouteurSSH dhcpd[1306]: Config file: /etc/dhcp/dhcpd.conf
Oct 15 18:53:26 RouteurSSH dhcpd[1306]: Database file: /var/lib/dhcpd/dhcpd.leases
Oct 15 18:53:26 RouteurSSH dhcpd[1306]: PID file: /var/run/dhcpd.pid
Oct 15 18:53:26 RouteurSSH dhcpd[1306]: Source compiled to use binary-leases
Oct 15 18:53:26 RouteurSSH dhcpd[1306]: Wrote 0 leases to leases file.
Oct 15 18:53:26 RouteurSSH dhcpd[1306]: Listening on LPF/enp0s8/08:00:27:7f:a8:40/10.5.1.0/24
Oct 15 18:53:26 RouteurSSH dhcpd[1306]: Sending on   LPF/enp0s8/08:00:27:7f:a8:40/10.5.1.0/24
Oct 15 18:53:26 RouteurSSH dhcpd[1306]:
Oct 15 18:53:26 RouteurSSH dhcpd[1306]: No subnet declaration for enp0s3 (10.0.2.15).
Oct 15 18:53:26 RouteurSSH dhcpd[1306]: ** Ignoring requests on enp0s3.  If this is not what
Oct 15 18:53:26 RouteurSSH dhcpd[1306]:    you want, please write a subnet declaration
Oct 15 18:53:26 RouteurSSH dhcpd[1306]:    in your dhcpd.conf file for the network segment
Oct 15 18:53:26 RouteurSSH dhcpd[1306]:    to which interface enp0s3 is attached. **
Oct 15 18:53:26 RouteurSSH dhcpd[1306]:
Oct 15 18:53:26 RouteurSSH dhcpd[1306]: Sending on   Socket/fallback/fallback-net
Oct 15 18:53:26 RouteurSSH dhcpd[1306]: Server starting service.
Oct 15 18:53:26 RouteurSSH systemd[1]: Started DHCPv4 Server Daemon.
``````
### B. Test avec un nouveau client

☀️ **Créez une nouvelle machine client `client3.tp5.b1`**
``````
[askun@clientpc3 ~]$ sudo nano /etc/sysconfig/network-scripts/ifcfg-enp0s8

DEVICE=enp0s3
NAME=client3

ONBOOT=yes
BOOTPROTO=dhcp

GATEWAY=10.5.1.254
DNS1=1.1.1.1
``````

``````
Oct 15 19:59:09 RouteurSSH dhcpd[1414]: Sending on   Socket/fallback/fallback-net
Oct 15 19:59:09 RouteurSSH dhcpd[1414]: Server starting service.
Oct 15 20:02:15 RouteurSSH dhcpd[1414]: DHCPREQUEST for 10.0.2.15 from 08:00:27:c1:4f:9a via enp0s8: wrong network.
Oct 15 20:02:15 RouteurSSH dhcpd[1414]: DHCPNAK on 10.0.2.15 to 08:00:27:c1:4f:9a via enp0s8
Oct 15 20:02:15 RouteurSSH dhcpd[1414]: DHCPDISCOVER from 08:00:27:c1:4f:9a via enp0s8
Oct 15 20:02:16 RouteurSSH dhcpd[1414]: DHCPOFFER on 10.5.1.137 to 08:00:27:c1:4f:9a (clientpc3) via enp0s8
Oct 15 20:02:16 RouteurSSH dhcpd[1414]: DHCPREQUEST for 10.5.1.137 (10.5.1.254) from 08:00:27:c1:4f:9a (clientpc3) via enp0s8
Oct 15 20:02:16 RouteurSSH dhcpd[1414]: DHCPACK on 10.5.1.137 to 08:00:27:c1:4f:9a (clientpc3) via enp0s8
lines 115-164/164 (END)
``````

# Cisco router main config

sudo usermod -a -G uucp USERNAME
gtkterm

```bash

enable
write erase
reload

enable
conf t
service password-encryption
aaa new-model
aaa authentication login default local
username имя privilege 15 secret пароль

conf t
hostname R1

conf t
interface Fa 4
ip address 202.155.101.2 255.255.255.252 // Данные провайдера
 либо ip address dhcp
no shutdown

conf t
interface Vlan 1
Ip address 192.168.0.1 255.255.255.0
no shutdown

ip route 0.0.0.0 0.0.0.0 202.155.101.1

ip dhcp pool LAN (LAN - имя пула)
network 192.168.0.0 255.255.255.0 (сеть из которой будем раздавать)
dns-server 192.168.0.1 8.8.8.8  (DNS сервера для клиентов)
default-router 192.168.0.1 (шлюз)
exit
ip dhcp excluded-address 192.168.0.1 192.168.0.100 (исключим первые сто адресов из DHCP)

ip domain-lookup
ip dns server
ip name-server 192.168.2.1  (провайдерский DNS)
ip name-server 8.8.8.8 (dns Google)

ip access-list standard ACL_NAT
permit 192.168.0.0 0.0.0.255
Interface Vlan 1
ip nat inside
Interface Fa 4
ip nat outside
ip nat inside source list ACL_NAT interface fa4

write

```
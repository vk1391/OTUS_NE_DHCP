# DHCPv4
![alt-dtp](https://github.com/vk1391/OTUS_NE_DHCP/blob/main/dhcp1.jpg "Схема к домашнему заданию №3")

**Устройство** | **Интерфейс** | **ip address** | **Маска подсети**
 --- | --- | --- | --- 
| R1 | e0/0 | 10.0.0.1 | 255.255.255.252
|    | e0/1 | n\a | n/a
|    | e0/1.100 | 192.168.1.1 | 255.255.255.192
|    | e0/1.200 | 192.168.1.65 | 255.255.255.224
|    | e0/1.1000 |  | 
| R2 | e0/0 | 10.0.0.2 | 255.255.255.252
|    | e0/1 |  192.168.1.97 | 255.255.255.240   
| S1 | vlan200 | 192.168.1.66 | 255.255.255.192  
| S2 | vlan1 | 192.168.1.98 | 255.255.255.240  

 - дефолтные настройки маршрутизаторов:
   ```
   hostname R1
   no ip domain-lookup 
   enable secret class
   line console 0
   password cisco
   login
   exit
   line vty 0 4
   password cisco
   login
   exit 
   service password-encryption 
   banner motd $ Authorized Users Only! $
   clock timezone UTC 3 
   ```
- дефолтные настройки коммутаторов:
  ```
  hostname S1
  no ip domain-lookup 
  enable secret class
  line console 0
  password cisco
  login
  exit
  line vty 0 4
  password cisco
  login
  exit 
  service password-encryption 
  banner motd $ Authorized Users Only! $
  clock timezone UTC 3 
  ```
- Конфигурация R1:
  ```
  R1(config)#do sh run
  Building configuration...
  
  Current configuration : 1610 bytes
  version 15.4
  service password-encryption
  hostname R1
  boot-start-marker
  boot-end-marker
  enable secret 5 $1$LQGj$a0cP5XypWeo.f/fEdf22T/
  no aaa new-model
  clock timezone UTC 3 0
  mmi polling-interval 60
  no mmi auto-configure
  no mmi pvc
  mmi snmp-timeout 180
  ip dhcp excluded-address 192.168.1.1 192.168.1.5
  ip dhcp excluded-address 192.168.1.97 192.168.1.101
  ip dhcp pool 1
   network 192.168.1.0 255.255.255.192
   domain-name ccna-lab.com
   default-router 192.168.1.1 
  lease 2 12 30
  ip dhcp pool 2
   network 192.168.1.96 255.255.255.240
   domain-name ccna-lab.com
   default-router 192.168.1.97 
   lease 2 12 30
  no ip domain lookup
  ip cef
  no ipv6 cef
  interface Ethernet0/0
   ip address 10.0.0.1 255.255.255.252
  interface Ethernet0/0.1
  interface Ethernet0/1
   no ip address
  interface Ethernet0/1.100
   encapsulation dot1Q 100
   ip address 192.168.1.1 255.255.255.192
  interface Ethernet0/1.200
   encapsulation dot1Q 200
   ip address 192.168.1.65 255.255.255.224
  interface Ethernet0/2
   no ip address
   shutdown
  interface Ethernet0/3
   no ip address
   shutdown
  ip forward-protocol nd
  no ip http server
  no ip http secure-server
  ip route 192.168.1.96 255.255.255.240 10.0.0.2
  
  ```

- Конфигурация R2:

 ```
  service timestamps debug datetime msec
  service timestamps log datetime msec
  service password-encryption
  hostname R2
  boot-start-marker
  boot-end-marker
  enable secret 5 $1$9Rkm$v8f6R0luH1x9EEtNvtGsv1
  no aaa new-model
  clock timezone UTC 3 0
  mmi polling-interval 60
  no mmi auto-configure
  no mmi pvc
  mmi snmp-timeout 180
  no ip domain lookup
  ip cef
  no ipv6 cef
  multilink bundle-name authenticated
  interface Ethernet0/0
   ip address 10.0.0.2 255.255.255.252
  interface Ethernet0/1
   ip address 192.168.1.97 255.255.255.240
   ip helper-address 10.0.0.1
  interface Ethernet0/2
   no ip address
   shutdown
  interface Ethernet0/3
   no ip address
   shutdown
  ip forward-protocol nd
  no ip http server
  no ip http secure-server
 ```
- Конфигурация S1:
 ```
 interface Ethernet0/0
  switchport trunk encapsulation dot1q
  switchport mode trunk
 !
 interface Ethernet0/1
  switchport access vlan 100
  switchport mode access
 !
 interface Ethernet0/2
 !
 interface Ethernet0/3
 !
 interface Vlan200
  ip address 192.168.1.66 255.255.255.192
 !
 ip forward-protocol nd
 !
 no ip http server
 no ip http secure-server
```
- Конфигурация S2
```
interface Ethernet0/0
!
interface Ethernet0/1
 switchport mode access
!
interface Ethernet0/2
!
interface Ethernet0/3
!
interface Vlan1
 ip address 192.168.1.98 255.255.255.240
!
ip forward-protocol nd
!
no ip http server
no ip http secure-server
```
- Получение IP VPC1:
```
VPCS> ip dhcp -r
DDORA IP 192.168.1.6/26 GW 192.168.1.1
```
- Получение IP VPC2:
```
VPCS> ip dhcp -r
DORA IP 192.168.1.103/28 GW 192.168.1.97
```



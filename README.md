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

#### Schemat rozwiązania
![alt text](https://github.com/Novachi/Sieci-Komputerowe/blob/master/zadanie-2/zadanie-2_diagram.png "Rysunek")

#### Określenie masek podsieci dla poszczególnych elementów modelu
* Każdy z routerów na danej kondygnacji potrzebuje możliwości posiadania co najmniej 4 hostów więc maska 255.255.255.248 (/29 - 6 możliwych hostów)

* Każda sala potrzebuje możliwości posiadania 35 hostów, więc maska 255.255.255.192 (/26 - 62 hosty)

* Dla wifi potrzeba maski umożliwiającej podłączenie 800 hostów wybierzemy zatem 255.255.252.0 (/22 - 1022 hosty)

#### Określenie adresów sieci

* Adres Bazowy: 188.156.220.160/27

* Router główny:
  * Kondygnacja 0: 188.156.220.224/29
  * Kondygnacja 1: 188.156.220.232/29
  * Kondygnacja 2: 188.156.220.240/29
  * Wifi: 188.156.221.0/27

* Router kondygnacji 0:
  * Sala 009: 10.0.9.0/26
  * Sala 013: 10.0.13.0/26
  * Sala 014: 10.0.14.0/26
  * Sala 017: 10.0.17.0/26
  
* Router kondygnacji 1:
  * Sala 115: 10.0.115.0/26
  * Sala 116: 10.0.116.0/26
  * Sala 117: 10.0.117.0/26
  * Sala 122: 10.0.122.0/26
  
* Router kondygnacji 2:
  * Sala 201: 10.0.201.0/26
  * Sala 202: 10.0.202.0/26
  * Sala 203: 10.0.203.0/26
  * Sala 204: 10.0.204.0/26
  
#### Konfiguracja interfejsów sieciowych i ustawienie routingu
Ustawiamy adresy ip, maski podsieci oraz routing za pomocą edytowania pliku /etc/network/interfaces
* Router główny:
  * enp0s8: 
    * address 188.156.221.1
    * netmask 255.255.255.224
  * enp0s9: 
    * address 188.156.220.241
    * netmask 255.255.255.248
  * enp0s10: 
    * address 188.156.220.233
    * netmask 255.255.255.248
  * enp0s11: 
    * address 188.156.220.225
    * netmask 255.255.255.248
    

* Router Kondygnacji 0:
  * enp0s3: 
    * address 188.156.220.226
    * netmask 255.255.255.248
    * up ip rotue add default via 188.156.220.225
  * enp0s8: 
    * address 10.0.9.1
    * netmask 255.255.255.192
  * enp0s9: 
    * address 10.0.13.1
    * netmask 255.255.255.192
  * enp0s10: 
    * address 10.0.14.1
    * netmask 255.255.255.192

  * enp0s11: 
    * address 10.0.17.1
    * netmask 255.255.255.192
 
W salach podłączonych do routera kondygnacji 0 adresy przydzieli DHCP. Odpowiednio: 10.0.[9 | 13 | 14 | 17].2 - 10.0.[9 | 13 | 14 | 17].62
 
Dodajemy również routing, odpowiednio: up ip rotue add default via 10.0.[9 | 13 | 14 | 17].1
 
* Router Kondygnacji 1:
  * enp0s3:
    * address 188.156.220.234
    * netmask 255.255.255.248
    * up ip rotue add default via 188.156.220.233
  * enp0s8: 
    * address 10.0.115.1
    * netmask 255.255.255.192
  * enp0s9: 
    * address 10.0.116.1
    * netmask 255.255.255.192

  * enp0s10: 
    * address 10.0.117.1
    * netmask 255.255.255.192

  * enp0s11: 
    * address 10.0.122.1
    * netmask 255.255.255.192

W salach podłączonych do routera kondygnacji 1 adresy przydzieli DHCP. Odpowiednio: 10.0.[115 | 116 | 117 | 122].2 - 10.0.[115 | 116 | 117 | 122].62
 
Dodajemy również routing, odpowiednio: up ip rotue add default via 10.0.[115 | 116 | 117 | 122].1

* Router Kondygnacji 2:
  * enp0s3:
    * address 188.156.220.242
    * netmask 255.255.255.248
    * up ip rotue add default via 188.156.220.241
  * enp0s8: 
    * address 10.0.201.1
    * netmask 255.255.255.192
  * enp0s9: 
    * address 10.0.202.1
    * netmask 255.255.255.192

  * enp0s10: 
    * address 10.0.203.1
    * netmask 255.255.255.192

  * enp0s11: 
    * address 10.0.204.1
    * netmask 255.255.255.192

W salach podłączonych do routera kondygnacji 0 adresy przydzieli DHCP. Odpowiednio: 10.0.[201 | 202 | 203 | 204].2 - 10.0.[201 | 202 | 203 | 204].62
 
 Dodajemy również routing, odpowiednio: up ip rotue add default via 10.0.[201 | 202 | 203 | 204].1
 
#### Forwarding
 Dla wszystkich routerów należy także włączyć forwarding odkomentowując wpis: net.ipv4.ip_forward=1 w pliku /etc/sysctl.d/99-sysctl.conf
 
#### Dodanie reguły MESQUERADE dla każdego routera
Aby tego dokonać wprowadzamy następujące polecenia w urządzeniach:
* Router Główny:
  * iptables -t nat -A POSTROUTING -s 188.156.220.224/29 -o enp0s3 -j MASQUERADE
  * iptables -t nat -A POSTROUTING -s 1188.156.220.232/29 -o enp0s3 -j MASQUERADE
  * iptables -t nat -A POSTROUTING -s 188.156.220.240/29 -o enp0s3 -j MASQUERADE
  * iptables -t nat -A POSTROUTING -s 188.156.221.0/22 -o enp0s3 -j MASQUERADE
* Router Kondygnacji 0:
  * iptables -t nat -A POSTROUTING -s 10.0.9.0/26 -o enp0s3 -j MASQUERADE
  * iptables -t nat -A POSTROUTING -s 10.0.13.0/26 -o enp0s3 -j MASQUERADE
  * iptables -t nat -A POSTROUTING -s 10.0.14.0/26 -o enp0s3 -j MASQUERADE
  * iptables -t nat -A POSTROUTING -s 10.0.17.0/26 -o enp0s3 -j MASQUERADE
                                 
* Router Kondygnacji 1:
  * iptables -t nat -A POSTROUTING -s 10.0.115.0/26 -o enp0s3 -j MASQUERADE
  * iptables -t nat -A POSTROUTING -s 10.0.116.0/26 -o enp0s3 -j MASQUERADE
  * iptables -t nat -A POSTROUTING -s 10.0.117.0/26 -o enp0s3 -j MASQUERADE
  * iptables -t nat -A POSTROUTING -s 10.0.122.0/26 -o enp0s3 -j MASQUERADE
  
* Router Kondygnacji 2:
  * iptables -t nat -A POSTROUTING -s 10.0.201.0/26 -o enp0s3 -j MASQUERADE
  * iptables -t nat -A POSTROUTING -s 10.0.202.0/26 -o enp0s3 -j MASQUERADE
  * iptables -t nat -A POSTROUTING -s 10.0.203.0/26 -o enp0s3 -j MASQUERADE
  * iptables -t nat -A POSTROUTING -s 10.0.204.0/26 -o enp0s3 -j MASQUERADE


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
  
#### Konfiguracja interfejsów sieciowych
Ustawiamy adresy ip i maski podsieci w /etc/network/interfaces
* Router główny:
 * enp0s9: 
   address 188.156.220.225
   netmask 255.255.255.248
   
 * enp0s10: 
   address 188.156.220.233
   netmask 255.255.255.248
   
 * enp0s11: 
   address 188.156.220.240
   netmask 255.255.255.248


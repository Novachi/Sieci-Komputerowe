![alt text](https://github.com/Novachi/Sieci-Komputerowe/blob/master/zadanie-1/zadanie1.png "Rysunek")

#### Ustalenie maski
LAN1 : 255.255.254.0 (/23 - 510 Hostów )

LAN2 : 255.255.224.0 (/19 - 8190 Hostów [/20 mieści tylko 4094 hostów])

#### Ustalanie adresów IP poszczególnych sieci
Adres bazowy : 172.22.128.0/17

LAN1 : 172.22.128.0/23

LAN2 : 172.22.160.0/19 (Z powodu tego że LAN1 zajmuje adresy na przestrzeni od 172.22.128.1 musimy wziąć adresy z kolejnej puli dostępnych przy masce /19 adresów którą są adresy od 172.22.160.1 - 172.22.191.254)

#### Ustawienie odpowiednich adresów, masek podsieci oraz routingu dla interfejsów
Aby to zrobić edytujemy plik /etc/network/interfaces w następujący sposób:

##### PC0
![alt text](https://github.com/Novachi/Sieci-Komputerowe/blob/master/zadanie-1/ipConfigPC0.PNG "PC0")

##### PC1
![alt text](https://github.com/Novachi/Sieci-Komputerowe/blob/master/zadanie-1/ipConfigPC0.PNG "PC0")

##### PC2
![alt text](https://github.com/Novachi/Sieci-Komputerowe/blob/master/zadanie-1/ipConfigPC0.PNG "PC0")

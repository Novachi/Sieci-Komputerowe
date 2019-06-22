#### Schemat rozwiązania
![alt text](https://github.com/Novachi/Sieci-Komputerowe/edit/master/zadanie-2/zadanie-2_diagram.png "Rysunek")

#### Określenie masek podsieci dla poszczególnych elementów modelu
* Każdy z routerów na danej kondygnacji potrzebuje możliwości posiadania co najmniej 4 hostów więc maska 255.255.255.248 (/29 - 6 możliwych hostów)

* Każda sala potrzebuje możliwości posiadania 35 hostów, więc maska 255.255.255.192 (/26 - 62 hosty)

* Dla wifi potrzeba maski umożliwiającej podłączenie 800 hostów wybierzemy zatem 255.255.252.0 (/22 - 1022 hosty)

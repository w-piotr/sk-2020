# Zadanie 2

Projekt sieci spełnił oczekiwania, organizacja po uwzględnieniu nowych wymogów chce podzielić dotychczasowe sieci na kilka podsieci.

1. Zaprojektuj oraz udokumentuj prototyp rozwiązania z wykorzystaniem oprogramowania ``CISCO Packet Tracer``, ``VirtualBox`` lub podobnego. 

## Schemat

![zadanie 2](stage-02.svg)

## Charakterystyka
  * LAN 1 pozostaje bez zmian
  * LAN 2 zostaje podzielony na 3 równe podsieci
  * LAN 3 zostaje podzielony na 3 podsieci z uwzględnieniem
    * podsieć 1 ma obsłużyć do 512 hostów
    * podsieć 2 ma obsłużyć do 10 hostów
    * podsieć 3 ma obsłużyć do 32 hostów
  * Usunięty został również link pomiędzy Routerem (LAN 1) a Routerem (LAN 2)
  * Uwzględnij zmiany w tablicy routingów

## Zawartość

 * Adresy poszczególnych sieci IP
 * Adresację linków pomiędzy routerami
 * Tablice routingów na poszczególnych routerach
 
 
# MODYFIKACJA!
 podsieć 1 ma obsłużyć do **512** hostów
 powinno być **510**
 


###Dokumentacja

##LAN 1

172.17.156.0/22 255.255.252.0

#Router 1

ethLan: 172.17.156.1 255.255.252.0

ethR1-R3: 10.10.10.5 255.255.255.252

----------Routing table----------

Dest|gateway
----|-------
172.17.12.0/22|10.10.10.6
172.17.200.0/22|10.10.10.6


##LAN 2

172.17.200.0/22 255.255.252.0

#Router 2

ethLan: 172.17.200.1 255.255.255.0

ethR2-R3: 10.10.10.9 255.255.255.252

----------Routing table----------

Dest|gateway
----|-------
172.17.12.0/22|10.10.10.10
172.17.156.0/22|10.10.10.10

##LAN 4

172.17.201.0/24 255.255.255.0

##LAN 5

172.17.202.0/24 255.255.255.0

##LAN 6

172.17.203.0/24 255.255.255.0

##LAN 3

172.17.12.0/22 255.255.252.0

#Router 3

ethLan: 172.17.12.1 255.255.255.0

ethR3-R1: 10.10.10.6 255.255.255.252

ethR3-R2: 10.10.10.10 255.255.255.252

----------Routing table----------

Dest|gateway
----|-------
172.17.156.0/22|10.10.10.5
172.17.200.0/22|10.10.10.9 

##LAN 7

172.17.14.0/23 255.255.254.0

##LAN 8 

172.17.13.176/28 255.255.255.240

##LAN 9 

172.17.13.192/26 255.255.255.192













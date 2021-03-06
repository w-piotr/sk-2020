## Konfiguracja route


* routing
    * dodaj trasę default
    * dodaj trasę przez bramę
    * dodaj trasę przez interfejs
    * usuń trasę
    * zmień trasę
    * pobierz trasę dla adresu
     
### ip 
| subcommand    |  polecenie   | opis  |
| ------------- |:-------------| :---------------| 
|   ``route``    |                               | |
|               |   ``ip route add``             | |


### Zastosowania

* Wydzielenie osobnej sieci dla urządzeń sieciowych
* Separacja urządzeń gościnnej sieci WIFI do osobnej sieci
* Zapewnienie komunikacji pomiędzy odrębnymi sieciami lokalnymi z wykorzystaniem VPN

![zadanie 4](example-network.svg)

### Zadanie

![zadanie 4](cwiczenia4.svg)

1.
   * Przygotuj konfigurację sieci zgodnie z powyższym diagramem, 
   * Przetestuj połączenie pomiędzy wszystkimi elementami sieci
   * Dlaczego połączenie może nie działać
   
Ad.1 

PC1 ip addr add 172.16.100.10/24 dev eth0
ping 172.16.100.1 - połączenie z routerem działa

PC0 ip addr add 172.16.100.1/24 dev eth0
PC0 ip addr add 10.0.10.1/24 dev eth1
ip link set eth1 up

PC3 ip addr add 10.0.10.10/24 dev eth0
ping 10.0.10.1 - połączenie z routerem działa

PC1 ip route add 10.0.10.0/24 via 172.16.100.1

PC3 ip route add default via 10.0.10.1

Jeżeli nie działa to znaczy, że nie jest ustawione przekazywanie pakietów.
Aby to zmienić na PC0:
echo 1 > /proc/sys/net/ipv4/ip_forward
lub sysctl net.ipv4.ip_forward=1


2. Przygotuj konfigurację tak aby została załadowana poprawnie po ponownym uruchomieniu systemu
   * Patrz ``utrwalanie statycznej konfiguracji cwiczenia 2``
   * zwróć uwagę na różnice pomiędzy dydtrybucjami systemu
3. Zainstaluj, uruchom i przetestuj działanie aplikacji ``chat``
   * aplikacja dostępna w serwisie github ``https://github.com/jkanclerz/client-server-chat`` lub preinstalowana na maszynie dostępnej w zasobach kursu


Ad.3
PC1
cd client-server-chat/
python3 server.py


PC3
cd client-server-chat/
python3 client.py 172.16.100.10 9999

### Zadanie do domu

1. Przygotuj konfigurację z zadania 1 wykorzystując inny system operacyjny na komputerze pełniącym rolę routera.
  * debian / centos / inny
  * zapewnij poprawną komunikację pomiędzy PC3 -> PC1
  
2. Dodaj kolejną sieć do komputera pełniącego funkcję routera
   * Sprawdź poprawność komunikacji pomiędzy innymi obszarami sieci
   * Zweryfikuj działanie programu chat pomiędzy różnymi segmentami sieci

![zadanie 4](todo.svg)


Rozwiązanie

PC1 ip addr add 172.16.100.10/24 dev eth0 ping 172.16.100.1 - połączenie z routerem działa

PC0 ip addr add 172.16.100.1/24 dev eth0
PC0 ip addr add 10.0.10.1/24 dev eth1
ip link set eth1 up
PC0 ip addr add 192.168.200.1/24 dev eth3
PC0 ip link set eth3 up

PC3 ip addr add 10.0.10.10/24 dev eth0 ping 10.0.10.1 - połączenie z routerem działa

PC1 ip route add 10.0.10.0/24 via 172.16.100.1
PC1 ip route add 192.168.200.0/24 via 172.16.100.1

PC3 ip route add 172.16.100.1/24 via 10.0.10.1
PC3 ip route add 192.168.200.0/24 via 10.0.10.1

PCX ip addr add 192.168.200.1/24 dev eth0
PCX ip route add 172.16.100.1/24 via 192.168.200.1
PCX ip route add 10.0.10.0/24 via 192.168.200.1

PCY ip addr add 192.168.200.1/24 dev eth0
PCY ip route add 172.16.100.1/24 via 192.168.200.1
PCY ip route add 10.0.10.0/24 via 192.168.200.1

Jeżeli nie działa to znaczy, że nie jest ustawione przekazywanie pakietów. Aby to zmienić na PC0: echo 1 > /proc/sys/net/ipv4/ip_forward lub sysctl net.ipv4.ip_forward=1

PC1 ping 10.0.10.10
PC1 ping 192.168.200.100
PC1 ping 192.168.200.101

PC3 ping 172.16.100.10
PC3 ping 192.168.200.100
PC3 ping 192.168.200.101

PCX ping 10.0.10.10
PCX ping 172.16.100.10
PCX ping 192.168.200.101

PCY ping 10.0.10.10
PCY ping 172.16.100.10
PCY ping 192.168.200.100

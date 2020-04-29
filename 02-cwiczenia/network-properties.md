## Ustawianie parametrów sieci

### Zadania

0. Z wykorzystaniem dowolnych systemów operacyjnych na których potrafisz uruchomić interpreter ``python`` oraz oprogramowania virtualbox odwzoruj poniższy schemat sieci:

![alt text][network]

[network]: ./network.png "Logo Title Text 2"

1. na 1 z komputerów zainstaluj i uruchom program ``server.py`` dostępne pod adresem ``https://github.com/jkanclerz/client-server-chat``
2. na 2 z komputerów zainstaluj i uruchom program ``client.py`` dostępne pod adresem ``https://github.com/jkanclerz/client-server-chat``
3. Manipulując konfiguracją sieci na poziomie virtualbox, uruchom serwer czatu, oraz udostępnij go na wybranym porcie oraz adresie tak aby istniała możliwość połączenia przez inne osoby w obrębie pracowni
4. Zainstaluj oprogramowanie serwera HTTP ``nginx`` lub innego, skonfiguruj plik index.html wg instrukcji, sprawdź dostępność strony z wykorzystaniem dowolnego klienta protokołu ``HTTP`` z różnych konfiguracji IP
5. Posługując się programami tj: ``netstat`` lub ``lsof`` sprawdź na jakich portach zostały uruchomione serwery czatu czy HTTP

Wejściowe parametry sieci
-------------------------
| Parametr | wartość | komentarz(opcionalny) |
| ------------- |:-------------:| -----:|
|   PC 1 |  
| IP - address  | 10.0.15.4 | |
| MASKA  | /24 (255.255.255.0) | |
|   |  | |
| PC 2  |  | |
| IP - address  | 10.0.15.6 | |
| MASKA  | /24 (255.255.255.0 )| |

Weryfikacja połączenia

Polecenie
```
ping 10.0.15.4 (z PC2) / ping 10.0.15.6 (z PC1)
```

Efekt
```
polecenie wyświetla ping
```

Statyczna konfiguracja parametrów połączenia
Wejściowe parametry sieci
-------------------------
| Parametr | wartość | komentarz(opcionalny) |
| ------------- |:-------------:| -----:|
|   PC 1 |  
| IP - address  | 192.168.10.10 | |
| MASKA  | 255.255.255.0 | |
|   |  | |
| PC 2  |  | |
| IP - address  | 192.168.10.11 | |
| MASKA  | 255.255.128.0 | |
| PC 2  |  | |
| IP - address  | 172.16.100.100 | |
| MASKA  | 255.255.0.0 | |

Weryfikacja połączenia

Polecenie
```
ping 192.168.10.10 (z PC2) / ping 192.168.10.11 (z PC1) / ping 172.16.100.100 (z PC1)
```

Efekt
```
działa / działa / nie działa
```

Nowa statyczna konfiguracja 

-------------------------
| Parametr | wartość | komentarz(opcionalny) |
| ------------- |:-------------:| -----:|
|   PC 1 |  
| IP - address  | 170.245.14.10 | |
| MASKA  | 255.255.255.0 | |
|   |  | |
| PC 2  |  | |
| IP - address  | 170.245.14.11/24 | |
| MASKA  | 255.255.255.0 | |

Weryfikacja połączenia

Polecenie
```
należy otworzyć vi etc/network/interfaces i ustawić
 iface eth0 inet static
        address 170.245.14.10
        netmask 255.255.255.0
 następnie rc-service networking restart żeby przeładować serwis sieci
```

Efekt
```
komunikacja działa po restarcie serwisów/maszyny
```

### Utrwalenie konfiguracji

Dlaczego? Jak? Co? :)

Konfiguracja jest utrwalona ponieważ została zapisana w pliku konfiguracyjnym skąd  może zostać załadowna.

### Warto wiedzieć

-------------------------
| Parametr | wartość | komentarz(opcionalny) |
| ------------- |:-------------:| -----:|
| Lokalizacja pliku z konfiguracją sieci| etc/network/interfaces | |
| UP -> Wyłączenie interfejsu sieciowego| ip link eth[X] up | |
| DOWN -> Włączenie interfejsu sieciowego| ip link eth[X] down | |
| Sprawdzenie obecnych parametrów | netstat | |
| lista wszystkich interfejsów | ip link show | |
| Które interfejsy jakie porty słuchają | netstat -l | -lt dla portów tcp, -ltpn nazwa programu bez nazw danch protokołów |


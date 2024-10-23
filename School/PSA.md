# PSA
Poznamky ku predmetu Python v Sietovych Aplikaciach

# Sockety
Socket je nastroj na komunikaciu medzi procesmi cez siet/v ramci jedneho PC  

Pri vytvarani socketu sa specifikuje domena socketu a typ socketu  

```python
import socket

sock = socket.socket((DOMENA, TYP))
```

## Domena socketu
- `AF_INET`
    - pracuje na sietovej vrstve (**L3**)
    - IPv4
- `AF_INET6`
    - pracuje na sietovej vrstve (**L3**)
    - IPv6
- `AF_PACKET`
    - pracuje na linkovej vrstve (**L2**)
    - Ethernet

## Typ socketu
- `SOCK_STREAM`
    - TCP
    - vytvori Ethernet, IP a TCP hlavicku
- `SOCK_DGRAM`
    - UDP
    - vytvori Ethernet, IP a UDP hlavicku
- `SOCK_RAW`
    - pracuje na nizsej urovni
    - hlavicky musim vytvorit sam
        - pri pouziti s `AF_PACKET` vytvaram Ethernet hlavicku
        - pri pouziti s `AF_INET` alebo `AF_INET6` vytvarame IP hlavicku

---

Cize finalne vytvorenie socketu moze vyzerat nejak takto...

```python
sock = socket.socket((AF_INET, SOCK_STREAM))
```

## Priklad 
### Server
```python
import socket

IP = "0.0.0.0"  # ip adresa, na ktorej bude pocuvat - v tomto pripade vsetky adresy
PORT = 9999  # port na ktorom bude pocuvat

sock = socket.socket((AF_INET, SOCK_STREAM))  # vytvorenie socketu
sock.bind((IP, PORT))  # 'aktivacia' socketu?
sock.listen(10)  # 10 = pocet cakajucich vo fronte

while True:
    (client_sock, (client_addr, client_port)) = sock.accept()  # prijimanie sprav
    ...
    client_sock.close()

sock.close()
```

### Klient
```python
import socket

SERVER_IP = 127.0.0.1
SERVER_PORT = 9999

sock = socket.socket((AF_INET, SOCK_STREAM))  # vytvorenie socketu
sock.connect((SERVER_IP, SERVER_PORT))

sock.send("Toto je moja uzasna sprava ktoru poslem na server".encode())  
sock.recv(1000)  # prijimanie zo servera; 1000 = buffer na prijmanie = 1000 B
```


# Poradie bajtov
Poradie bajtov pri prenose udajov cez siet zavisi od architektury procesora  

## Big-endian
"Najvyznamnejsi" bajt (prvy) sa ulozi na miesto s najnizsou adresou (normalne)  
Napr. sprava `01234567` by bola rozdelena na `01` - `23` - `45` - `67`  
Pouzivaju architektury ako PowerPC, SPARK, ARM a sietove zariadenia  

## Little-endian
"Najmenej vyznamny" bajt (posledny) sa ulozi na miesto s najnizsou adresou  
Napr. sprava `01234567` by bola rozdelena na  `67` - `45` - `23` - `01`  
Pouzivaju architektury x86 a ARM  


